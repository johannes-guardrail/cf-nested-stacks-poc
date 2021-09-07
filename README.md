# Cloudformation Nested Stack Test

## Create the bucket (run once)

```
aws s3 mb s3://cf-guardrail-us-west-2
```

## Package your file
```
aws cloudformation package \
  --template-file main.yaml \
  --s3-bucket cf-guardrail-us-west-2 \
  --output-template-file packaged.yaml
```


## Deploy packaged file
```
aws cloudformation deploy \
  --stack-name Nested-Test  \
  --region us-west-2  \
  --template-file packaged.yaml \
  --parameter-overrides EnvironmentName=Test-CF-Environment \
  --capabilities CAPABILITY_IAM
```

## Remove Stack

```
aws cloudformation delete-stack --stack-name Nested-Test
aws cloudformation wait stack-delete-complete --stack-name Nested-Test
```