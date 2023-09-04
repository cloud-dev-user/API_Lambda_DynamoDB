# API_Lambda_DynamoDB

This Github repo s created from AWS refrence page : 
https://docs.aws.amazon.com/lambda/latest/dg/services-apigateway-tutorial.html#services-apigateway-tutorial-test-setup 


1. Create Policy for lambda and API gateway: lambda-apigateway-policy
2. Create Role for lambda and API gateway: lambda-apigateway-role
3. Create lambda function using python : LambdaFunctionOverHttps.py
4. Create json file : " input.txt"  and test lambda function
5. Invoke Lambda function using followng aws cli command
   $ aws lambda invoke --function-name LambdaFunctionOverHttps --payload file://input.txt outputfile.txt --cli-binary-format raw-in-base64-out
6. Go to AWS API gateway console and create RESTAPI "DynamoDBOperations"
7. Again , using AWS API gateway console, create resource  -  
     Resource Name - DynamoDBManager
     Resource Path - /dynamodbmanager
8. Create an HTTP POST method for your "DynamoDBManager" resource.
      Setup:
             Integration type --> Lambda Function
             Lambda Region  --> Same Region as your Lambda function
             Lambda Function  --> LambdaFunctionOverHttps
             Add Permission to Lambda Function  --> click ok
9. Create a DynamoDB table
            Table name --> lambda-apigateway
            Partition key  --> id
            Data type --> String

10. Test the integration of API Gateway, Lambda, and DynamoDB using "json request body" file from API gateway console
11. Deploy the API
      API gateway Console --> DynamoDBOperations --> Actions --> Deploy API --> Deployment stage --> new stage
       Stage name: test  --> Invoke API
12. invoke the Lambda function using curl to add data to dynamoDB 
       $ curl https://l8togsqxd8.execute-api.us-west-2.amazonaws.com/test/dynamodbmanager -d '{"operation": "create", "payload": {"Item": {"id": "5678EFGH", "number": 15}}}'

13. Invoke the Lambda function using curl to delete data to dynamoDB
      $ curl https://l8togsqxd8.execute-api.us-west-2.amazonaws.com/test/dynamodbmanager -d '{"operation": "delete", "payload": {"Key": {"id": "5678EFGH"}}}'
    
    








   
