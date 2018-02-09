# Install cross-env to help configure environment
`npm install cross-env --save-dev`

Update `npm test` script in `package.json`

this will set the `NODE_ENV` to test environment

```
  "scripts":{
    "start": "node server.js",
    "test":"cross-env NODE-ENV=test mocha"
  }
```
# Add a `test` property to knexfile.js

```
  module.exports = {
    test:{
      client: 'pg',
      connection:process.env.TEST_DATABASE_URL || 'postgres://postgres:5408@localhost/noteful_test'
      debug: true, // http://knexjs.org/#Installation-debug
      pool: {min : 1 , max : 2}
    }
  }
```

# update server.test.js files to verify environment

after `REALITY CHECK`;

```   
  describe('Environment', () => {
    it('NODE_ENV should be "test"', () => {
      expect(process.env.NODE_ENV).to.equal('test');
    });
    it('connection should be test database', () => {
      expect(knex.client.connectionSettings.database).to.equal('noteful-test');
    });
  });
```

# Configure Test Hooks to seed test database before and after test

```
      const knex = require('../knex')
      const seedData = require('../db/seed')
      before(function () {
        // noop
      });

      beforeEach(function () {
        return seedData()
      })

      afterEach(function () {
        // noop
      })

      after(function () {
        // destroy the connection
        return knex.destroy();
      })
```