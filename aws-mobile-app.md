# My first AWS Project
## Components
1. CloudFormation - Builds other compoments of apps from templates. This includes the CodeStart project and the serverless app components
2. CodeStar - CodeStar is a centralized location made up of CodeCommit, CodeBuild, and CodePipeline
    1. CodeCommit is a git repo
    2. CodeBuild builds code
    3. CodePipeline checks out the code, builds it, and pushes it to CloudFormation to be built
3. API Gateway - Exposes API to lambda functions
4. Lambda - Serverless code running java
5. DynamoDB - NoSQL database
6. IAM - identity and access management
7. S3 - Super simple storage. Holds templates and jars
8. Mobile Hub - A set of services to make mobile app development easier. Use this to set up Cognito and pointed at the API gateway to generate a mobile SDK
9. android and iOS mobile apps
10. CloudWatch - logging

## Getting Started
A lot of the set up was done by using the CodeStar service. Creating a new CodeStart project sets up two templates in CloudFoundation. The first template builds out the CodeStar project. This includes all neccessary IAM roles, permissions, and policies as well as the CodeCommit repo, CodeBuild instance, and CodePipeline. The second template creates the actual serverless app components. Again includes the IAM pieces, as well as starter lambda functions. You're then able to add any components you want including an API Gateway, additional permissions, and DynamoDB tables. 

## The Generated Project
The project created by CodeStar has a couple of components. 
1. Lambda functions in a standard java package structure
2. The project is initially structured as a maven project so you'll have a pom file for dependencies
3. A template.yml file that tells CloudFormation how to build your serverless app
4. A buildspec.yml that tells CodeBuild how to do it's job

## The Code (basics)
The lambda functions are simple to implement. You just have to implement the RequestHandler interface. Serialization, authorization, authentication, etc are handled by AWS for you. I'll go over how to externalize configuration and db setup in a different section

## The Template
The template is made up of a few types of components
1. The declration of the API, which is configured in a swagger.yml file
2. A policy that gives permissions to the DynamoDB tables
3. The lambda execution role for lambda fuctions to assume
4. The declaration of the lambda functions
5. The declaration of the DynamoDB tables

## The Swagger File
The swagger file defines the API Gateway. It's a standard swagger definition except for the aws integration which defines how the API will interact with the lambda functions

## The Buildspec & Pipeline
Steps the build process takes
1. On every push to CodeCommit, CodePipeline pulls the code and sends it to CodeBuild
2. We change to the aws directory because the code to build is in a sub directory of the project
3. A standard mvn build is executed which outputs a jar file
4. The AWS package formation then processes the template so it's in a format acceptable by CloudFormation
5. The deploy step takes the template as an input which is then pushed to CloudFormation. The jar and swagger file already available for CloudFormation on S3

