# amplify-helpers

```
amplify add function 

```

add permissions to api, auth

### amplify/backend/function/{FUNCTION_NAME}/src/index.js
```javascript
// Put your code below this line.

/* Amplify Params - DO NOT EDIT
	API_EXAMPLE_GRAPHQLAPIENDPOINTOUTPUT
	API_EXAMPLE_GRAPHQLAPIIDOUTPUT
	AUTH_EXAMPLE_USERPOOLID
	ENV
	REGION
Amplify Params - DO NOT EDIT */

require("isomorphic-fetch");
const AUTH_TYPE = require('aws-appsync').AUTH_TYPE;
const AWSAppSyncClient = require('aws-appsync').default;

exports.handler = async (event) => {

const graphqlClient = new appsync.AWSAppSyncClient({
  url: 'APPSYNC_ENDPOINT_URL',
  region: process.env.AWS_REGION,
  auth: {
    type: 'AWS_IAM',
    credentials: {
      accessKeyId: process.env.AWS_ACCESS_KEY_ID,
      secretAccessKey: process.env.AWS_SECRET_ACCESS_KEY,
      sessionToken: process.env.AWS_SESSION_TOKEN
    }
  },
  disableOffline: true
});

    
const createLogMutation =
    `mutation createLog($input: CreateLogInput!) {
        createLog(input: $input) {
            id
            event
            detail
        }
    }`;
    
let logDetails = {
        "event": "sample event",
        "detail": "sample detail"
      }
      
try {
    const result = await graphqlClient.mutate({
    mutation: gql(createLogMutation),
    variables: {input: logDetails}
});
    console.log(result.data);
    callback(null, result.data);
} catch (e) {
    console.warn('Error sending mutation: ',  e);
    callback(Error(e));

}
    return response;
};

```
### Install dependencies 
`yarn add isomorphic-fetch aws-appsync uuid graphql-tag graphql`
