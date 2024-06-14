
# DynamoDB Streams Example with Node.js

## Description

This repository provides an example of using DynamoDB Streams with Node.js. It demonstrates how to set up and use DynamoDB Streams for capturing and processing data changes in a DynamoDB table, which is useful for developers looking to implement real-time data processing in their applications.

## Requirements

- Node.js
- AWS Account with DynamoDB and DynamoDB Streams enabled
- AWS SDK for Node.js
- Yarn or npm for package management

## Mode of Use

1. Clone the repository:
   ```bash
   git clone https://github.com/ferrerallan/dynamodb-streams.git
   ```
2. Navigate to the project directory:
   ```bash
   cd dynamodb-streams
   ```
3. Install the dependencies:
   ```bash
   yarn install
   ```
4. Ensure you have AWS CLI configured with appropriate permissions.
5. Start the application to consume streams:
   ```bash
   node consumer.js
   ```

## Implementation Details

- **consumer.js**: Contains code to consume and process DynamoDB Streams.
- **package.json**: Configuration file for the Node.js project, including dependencies.

### Example of Use

Here is an example of how to set up a DynamoDB Streams consumer:

```javascript
const AWS = require('aws-sdk');
const ddbStreams = new AWS.DynamoDBStreams({ region: 'us-west-2' });

const params = {
  StreamArn: 'your_dynamodb_stream_arn',
  ShardIteratorType: 'LATEST'
};

ddbStreams.getShardIterator(params, (err, data) => {
  if (err) console.log(err, err.stack);
  else {
    const shardIterator = data.ShardIterator;
    const getRecordsParams = {
      ShardIterator: shardIterator
    };

    ddbStreams.getRecords(getRecordsParams, (err, data) => {
      if (err) console.log(err, err.stack);
      else console.log(data.Records);
    });
  }
});
```

This code initializes a DynamoDB Streams client, retrieves a shard iterator, and fetches records from the stream.

## License

This project is licensed under the MIT License.

You can access the repository [here](https://github.com/ferrerallan/dynamodb-streams).
