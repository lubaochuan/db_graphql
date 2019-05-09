source: https://graphql.org/graphql-js/running-an-express-graphql-server/

To experiment with a graphql database:
- clone this repository.
- run `npm install` in the project directory to install packages.
- start server with `npm index.js`.
- go to `https://database-baochuan.c9users.io/graphql` to use the web client.



To setup the project yourself:
- set up a new project by creating a directory
and running `npm init` in the directory.
- install packages by running
`npm install express express-graphql graphql --save`.
- copy the following code to `index.js`.
```
var express = require('express');
var graphqlHTTP = require('express-graphql');
var { buildSchema } = require('graphql');

// Construct a schema, using GraphQL schema language
var schema = buildSchema(`
  type Query {
    hello: String
  }
`);

// The root provides a resolver function for each API endpoint
var root = {
  hello: () => {
    return 'Hello world!';
  },
};

var app = express();
app.use('/graphql', graphqlHTTP({
  schema: schema,
  rootValue: root,
  graphiql: true,
}));

/*
app.listen(4000);
console.log('Running a GraphQL API server at localhost:4000/graphql');
*/

var port = process.env.PORT;
var IP = process.env.IP;
app.listen(port, IP, () => {
  console.log('Listening on port '+process.env.PORT);
});

```