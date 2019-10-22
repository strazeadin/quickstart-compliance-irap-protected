# IRAP PROTECTED Reference Architecture #

## Design Overview ##

The Reference Architecture demonstrates how multiple AWS services are brought together to support a typical multi-tier web application with associated security and management services that meet ISM PROTECTED control requirements.

It is based on the Reference Architecture that is outlined in the IRAP PROTECTED Package that is available from [AWS Artifact](https://aws.amazon.com/artifact/).

## How to Deploy ##

1. Upload this [Lambda zipfile](https://s3.amazonaws.com/exampleloadbalancer-us-east-1/blog-posts/static-ip-for-application-load-balancer/populate_NLB_TG_with_ALB.zip) to the S3 bucket you specify in your LambdaZIPBucket parameter. This Lambda will automatically point your Network Load Balancer (NLB) to your Application Load Balancer (ALB).
1. If you're planning on using the ALB/NLB integration, you'll need to make a small change to this Lambda function. Open up the Lambda console and change line 230 from this:
  `dns_lookup_result = dns_lookup(ALB_DNS_NAME, "A", authoritative_server_ip_list)`

   To this:
  `dns_lookup_result = dns_lookup(ALB_DNS_NAME, "A")`
   
   This will use the internal VPC DNS to lookup the ALB's IP addresses, rather than the public DNS resolvers for the region. We have to change this because our Lambda function is running in the VPC.
1. [Import your own certificate](https://docs.aws.amazon.com/acm/latest/userguide/import-certificate.html) or [request a public certificate](https://docs.aws.amazon.com/acm/latest/userguide/gs-acm-request-public.html) for your ALB by using [AWS Certificate Manager](https://aws.amazon.com/certificate-manager/).
1. Populate the parameters in `parameters.json` with your own values.
1. Copy `master.yaml` to an S3 bucket either through the AWS Console or by running this command:
    
    `aws s3 cp master.yaml s3://<<LAMBDA_ZIPBUCKET>>/master.yaml`

1. Run CloudFormation either through the AWS Console or by running this command:

    `aws cloudformation create-stack --template-url https://s3.amazonaws.com/<PATH TO YOUR BUCKET>/master.yaml --stack-name protected-cfn --parameters file://parameters.json --capabilities CAPABILITY_IAM CAPABILITY_AUTO_EXPAND`

1. Check whether GuardDuty is enabled in your region. If it is already enabled, you should comment out the AWS::GuardDuty::Detector in the template or it will cause your stack deployment to fail.

## Architecture Overview ##

This architecture implements the Reference Architecture outlined on page 12 of the `AWS PROTECTED - Reference Architecture.pdf` guidance within the IRAP PROTECTED Package that is available from [AWS Artifact](https://aws.amazon.com/artifact/).

This architecture uses both CloudFormation and the Serverless Application Model.

Includes the optional Network Load Balancer that is *only required for cross VPC use cases such as inter-agency usage*.

