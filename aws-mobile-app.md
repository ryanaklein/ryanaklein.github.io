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

## Getting started
A lot of the set up was done by using the CodeStar service. Creating a new CodeStart project sets up two templates in CloudFoundation. The first template builds out the CodeStar project. This includes all neccessary IAM roles, permissions, and policies as well as the CodeCommit repo, CodeBuild instance, and CodePipeline. The second template creates the actual serverles app components. Again includes the IAM pieces, as well as starter lambda functions. You're then able to add any components you want including an API Gateway, additional permissions, and DynamoDB tables. 
