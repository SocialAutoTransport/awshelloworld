# awshelloworld - custom integration "hello world" example from AWS docs
### with condensed instructions, original instructions at https://docs.aws.amazon.com/apigateway/latest/developerguide/getting-started-lambda-non-proxy-integration.html


## To create Lambda function:
1. Go to AWS console > Services > Compute > Lambda > Create Function > use UI to create new function with Node.js using existing Test role
2. Go to your new function, scroll down and paste node.js code in lambdafunction.js (in this repository) into index.js. Handler field should match name of module . name of handler function in module, in this case Handler = index.handler
3. In the Designer, add the trigger for API Gateway

## To configure the example API Gateway:
1. Go to Services > Networking & Content Delivery > API Gateway > Create API
2. Go to your new API, select ( / ), select Actions > Create Resource
3. Resource Path = {city}, then select Enble API Gateway Cors
4. Select ( /{city} ), select Actions > Create Method and choose "ANY"
5. In Method Setup, choose Lambda Function as Integration type, then type in the name of the Lambda function created earlier and Save
6. Select "ANY" method > Method Request
7. Under Settings > Request Validator, choose "Validate body, query string parameters, and headers"
8. Add "time" as a required query string parameter, add "day" as a required HTTP Request Header
9. Add "callerName" as a payload property under Request Body
        a. Under your API name, choose Models > Create
        b. Type in model name and application/json as content type
        c. Copy and paste schema into Model schema field from customintegrationmodel.json (in this repository)
        d. Return to your API config > "ANY" method > Method Request > Request Body > add model
        e. Content type is application/json and choose the name of your recently created schema in the dropdown under Model name
        
10. Select "ANY" method > Integration Request > Mapping Templates
11. For Request body passthrough, select "When there are no templates defined"
12. Add mapping template with content type application/json and copy and paste mapping template from mapping.json (in this repository)

## Test directly in AWS or with Postman, specifying all required parameters
### to use AWS testing feature, visible under selected method "ANY"
Example test:
1. choose POST method
2. Path: /Richmond?time=morning
3. Headers: day:Wednesday
4. Request Body:
   {
    "callerName":"Eliza"
    }

        
        

