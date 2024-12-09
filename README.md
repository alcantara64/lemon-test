# API Sample Test

## Getting Started

This project requires a newer version of Node. Don't forget to install the NPM packages afterwards.

You should change the name of the `.env.example` file to `.env`.

Run `node app.js` to get things started. Hopefully the project should start without any errors.

## Explanations

The actual task will be explained separately.

This is a very simple project that pulls data from HubSpot's CRM API. It pulls and processes company and contact data from HubSpot but does not insert it into the database.

In HubSpot, contacts can be part of companies. HubSpot calls this relationship an association. That is, a contact has an association with a company. We make a separate call when processing contacts to fetch this association data.

The Domain model is a record signifying a HockeyStack customer. You shouldn't worry about the actual implementation of it. The only important property is the `hubspot`object in `integrations`. This is how we know which HubSpot instance to connect to.

The implementation of the server and the `server.js` is not important for this project.

Every data source in this project was created for test purposes. If any request takes more than 5 seconds to execute, there is something wrong with the implementation.

# Debrief

1. Introduce Typescript for type safety and implement object oriented approach
2. Implement the solid design principles for a more dry code, the `worker.js` serve to many purpose
3. Transition to an event driven mode using AWS SQS or RabbitMq for queue management
4. Distribute processing across multiple worker instances, using tools like kubernetes to handle horizontal scaling
5. Replace console.log statements with a logging framework like Winston
6. The saveDomain method marks the domain as modified and saves the entire object, this could be optimized by saving only the change field ($set in Mongodb) to reduce the database write load.
7. The current implementation processes contacts, companies, and meetings sequentially, which can cause delays in syncing. Using parallel promises with appropriate batching (e.g., Promise.allSettled for batched API calls) would significantly improve performance.
8. Implement catching using redis and help improve performance for a larger amount of data
