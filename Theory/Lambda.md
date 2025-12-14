## AWS Lambda 
Lambda is AWS’s serverless compute service.
It lets you run code without managing servers, paying only for execution time.
How it works: write the code and AWS runs it when triggered.
Triggers are:
- API Gateway HTTP requests
- S3 uploads
- DynamoDB streams
- CloudWatch events
- SNS messages
- EventBridge rules
- Direct invocation

Lambda execution typically lasts milliseconds to seconds, not hours.

#### Lambda key concepts
1. Runtime - the language function is written in
2. Handler Function - Lambda expects a function entry point
Ex: def lambdahandler(event, context):
    return {"statusCode"=200, "body":"Hello"}
3. Event object - Contains data passed to lambda
4. context object - has metadata: function name, timeout, request ID
5. Cold start vs warm start - Lambda uses execution environments. The first call may have a cold start; subsequent calls reuse the environment, to reduce latency.

## Amazon API Gateway
API Gateway is a fully managed service for creating, securing, and scaling APIs.
It is used to:
- Receive HTTP requests
- Route them to Lambda, ECS, EC2, or backend services
- Handle authentication & rate limiting
- Transform requests & responses
- Provide custom domains