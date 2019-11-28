# Infra Cloud - Cloud Formation

## Pre Req

Validate CF Templates

` $ aws cloudformation validate-template --template-body file://MainStack.yml `

` $ aws cloudformation validate-template --template-body file://SubnetStack.yml `

` $ aws cloudformation validate-template --template-body file://NatGatewayStack.yml `

Create a bucket of CF Templates

` $ aws s3 mb s3://cf-templates/ --region us-east-1 `

Sync the git repo to bucket of CF Templates

` $ aws s3 sync . s3://cf-templates/ --region us-east-1 `

Deploy CF Stack

` $ aws cloudformation deploy --region us-east-1 --stack-name baconStack --template-file MainStack.yml --capabilities CAPABILITY_NAMED_IAM --parameter-overrides CIDRRange=12.0.0.0/20 PrivateSubnetAZ1=12.0.0.0/25 PrivateSubnetAZ2=12.0.1.0/25 PublicSubnetAZ1=12.0.2.0/26 PublicSubnetAZ2=12.0.2.128/26 PeerVPCId=vpc-2f984855 PeeringCIDRRange=172.31.0.0/16 Prefix=dev`

Delete CF Stack

` $ aws cloudformation delete-stack --region us-east-1 --stack-name baconStack `