# netcore-lambda

Short introduction to AWS Lambda tooling with .NET Core.

## What is lambda

> AWS Lambda lets you run code without provisioning or managing servers. You pay only for the compute time you consume.
>
> With Lambda, you can run code for virtually any type of application or backend service - all with zero administration. Just upload your code and Lambda takes care of everything required to run and scale your code with high availability. You can set up your code to automatically trigger from other AWS services or call it directly from any web or mobile app.

[AWS Lambda documentation](https://aws.amazon.com/lambda/)

> AWS Lambda is a solution to reduce this wastage of resources.

[AWS Lambda overview](https://dashbird.io/blog/aws-lambda-overview-for-dummies/)

## Lambda and .Net Core tooling

AWS offers good tooling around Lambdas for dotnet.

```bash
dotnet tool install -g Amazon.Lambda.Tools
```

Available templates can be viewed

```bash
dotnet new lambda --list
```

[AWS Lambda for .NET Core - Github](https://github.com/aws/aws-lambda-dotnet)

### Create new API Lambda

Create new project with lambda template.

```bash
dotnet new serverless.AspNetCoreWebAPI -n demoapi --profile default
```

Deploy to AWS.

```bash
dotnet lambda deploy-serverless
```

Check running lambdas.

```bash
dotnet lambda list-serverless
```

Delete lambda

```bash
dotnet lambda delete-serverless
```

### Debugging lambdas locally

Possibilities for running Lambdas (and other AWS services) locally exist.

- [Serverless framework](https://www.serverless.com/)
- [AWS SAM local](https://github.com/thoeni/aws-sam-local)
- [Docker-lambda](https://github.com/lambci/docker-lambda)
- [LocalStack](https://github.com/localstack/localstack)

However, if you just want to debug your lambda the above might be overkill.

For that purpose we can use AWS .NET Mock lambda test tool.

Install the mock tool.

```bash
dotnet tool install -g Amazon.Lambda.TestTool-3.1
```

Create new lambda with something that is harder to test locally otherwise.

```bash
dotnet new lambda.SNS -n snstest --profile default
```

[AWS .NET Mock lambda test tool](https://github.com/aws/aws-lambda-dotnet/tree/master/Tools/LambdaTestTool)

#### Visual Studio configuration

```json
{
  "profiles": {
    "Mock Lambda Test Tool": {
      "commandName": "Executable",
      "commandLineArgs": "--port 5050",
      "executablePath": "c:\\Users\\opt\\.dotnet\\tools\\dotnet-lambda-test-tool-3.1.exe",
      "workingDirectory": ".\\bin\\Debug\\netcoreapp3.1"
    }
  }
}
```
