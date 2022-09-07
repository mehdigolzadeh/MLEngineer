# Copy file to s3 bucket inside jupyter notebook:

```
%%bash
aws s3 cp source s3://destination
```


# Create EKS cluster

```
$ aws configure
AWS Access Key ID [None]: key
AWS Secret Access Key [None]: secret
Default region name [None]: eu-central-1
Default output format [None]: json
```

Create yaml file "cluster-1.21.yaml":
```
apiVersion: eksctl.io/v1alpha5
kind: ClusterConfig
metadata:
  name: devops-catalog
  region: eu-central-1
  version: "1.21"
managedNodeGroups:
- name: linux-nodes
  instanceType: m5.xlarge
  minSize: 5
  maxSize: 10
```

Run command
```
 eksctl create cluster -f .\cluster-1.21.yaml
```

# Delete an EKS cluster
```
eksctl delete cluster --region=eu-central-1 --name=devops-catalog
```
