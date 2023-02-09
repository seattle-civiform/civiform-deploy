# Initial Deployment - CloudFormation

This guide is for SREs or DevOps folks. It explains how to do an initial deployment of CiviForm into your production cloud environment.


* Can be deployed directly into AWS, via direct AWS APIs and tools such as [cloudformation](https://github.com/civiform/civiform-deploy/tree/main/infra).

## Deploying into AWS using CloudFormation

Seattle's production infrastructure is managed declaratively by [cloudformation](https://github.com/seattle-civiform/civiform-deploy/tree/main/infra). To deploy, `run bin/deploy-prod`. You will need the AWS CLI - `brew install awscli`.

### Resources not managed by CloudFormation

#### DNS records

The records for civiformstage.seattle.gov and civiform.seattle.gov are created in and delegated to hosted zones managed via Route 53.

#### SSL Certificates

The SSL certificates for civiformstage.seattle.gov civiform.seattle.gov are managed by the City of Seattle and is stored in Certificate Manager. These must be manually imported. 

#### Notification endpoints

The messages for tickets or production failures are sent to SNS queues which are maintained by CloudFormation. The distribution lists of those queues are managed in the console.

#### Log processing

Our logs are processed by [this Lambda function](https://us-west-2.console.aws.amazon.com/lambda/home?region=us-west-2#/functions/prod-log-processor?tab=code), which is also managed by the console. You'll need to be signed in to the Civiform AWS account, which you can reach [here](https://seattle-commercial.awsapps.com/start#/).

The logging input is configured in [this panel](https://us-west-2.console.aws.amazon.com/lambda/home?region=us-west-2#/functions/prod-log-processor?tab=configure), and you can read more about how to work with Lambda and CloudWatch logs [here](https://docs.aws.amazon.com/lambda/latest/dg/welcome.html) and [here](https://docs.aws.amazon.com/lambda/latest/dg/services-cloudwatchlogs.html).
