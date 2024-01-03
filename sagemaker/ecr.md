# Useful commands

to list all the repositories:
```
aws ecr describe-repositories --registry-id [account_id]
```

to describe an image:
```
aws ecr describe-images --region eu-central-1 --registry-id [accountid] --repository-name [repo name->sagemaker-studio-decision-trees]
```
