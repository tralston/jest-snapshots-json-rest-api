# jest-snapshots-json-rest-api

[![Build Status](https://travis-ci.org/gillesdemey/jest-snapshots-json-rest-api.svg?branch=master)](https://travis-ci.org/gillesdemey/jest-snapshots-json-rest-api)
[![Coverage Status](https://coveralls.io/repos/github/gillesdemey/jest-snapshots-json-rest-api/badge.svg)](https://coveralls.io/github/gillesdemey/jest-snapshots-json-rest-api)

Jest Snapshots serializer for JSON REST APIs.

## Install

`yarn add --dev jest-snapshots-json-rest-api`

Add the following to your Jest configuration in `package.json`

```json
{
  "jest": {
    "snapshotSerializers": ["jest-snapshots-json-rest-api"]
  }
}
```

or manually add the snapshot serializer to your test suite:

```javascript
const serializer = require('jest-snapshots-json-rest-api')

// add the JSON REST API snapshot serializer
expect.addSnapshotSerializer(serializer)
```

## Usage

The object you want to snapshot **must** match the following struct for the serializer to work:

```javascript
{
  status: 200,
  body: {
  	hello: 'world'
  }
}
```

Modules like `supertest` work out-of-the-box. Also works with [`LightMyRequest`](https://github.com/fastify/light-my-request).

```javascript
const app = require('./app')
const request = require('supertest')

test('get a user', async () => {
  const response = await request(app)
    .get('/users/')

  expect(response.status).toBe(200)
  expect(response).toMatchSnapshot()
})
```

This will generate the corresponding `.snap` file:

```javascript
exports[`get a user 1`] = `{
  "hello": "world"
}
`;
```
