# Running the Demo

## Keypair
Create an EC2 Keypair in the desired region. Note the name.

## Launching the Stack

```bash
git clone https://github.com/dliggat/ecs-refarch-cloudformation.git
cd ecs-refarch-cloudformation

# Sync the templates
BUCKET=your-bucket
aws s3 mb s3://${BUCKET}
aws s3 sync . s3://${BUCKET}

# Launch the CloudFormation stack
KEYPAIR=your-keypair-name
STACKNAME=DemoECS

aws cloudformation create-stack  --stack-name ${STACKNAME} \
--template-body file://master.yaml                         \
--capabilities CAPABILITY_IAM CAPABILITY_NAMED_IAM         \
--parameters ParameterKey=TemplateBucket,ParameterValue=${BUCKET} ParameterKey=KeyName,ParameterValue=${KEYPAIR}
```

## Retrieve the Outputs

Retrieve the URL for the `ProductService` and `WebsiteService`.

```bash
aws cloudformation describe-stacks --stack-name ${STACKNAME} --query 'Stacks[0].Outputs'
```

