# Install cross-env to help configure environment
`npm install cross-env --save-dev`

Update `npm test` script in `package.json`
this will set the `NODE_ENV` to test environment
  `
    "scripts":{
      "start": "node server.js",
      "test":"cross-env NODE-ENV=test mocha"
    }
  `
