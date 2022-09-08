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
or
```
eksctl delete cluster  -f .\cluster-1.21.yaml --wait
```

# Get kubernetes node:
```
kubectl get nodes
```

# Install KUBEFLOW using kustomize
```
while ! kustomize build deployments/vanilla | kubectl apply -f -; do echo "Retrying to apply resources"; sleep 30; done
```




After installation, it will take some time for all Pods to become ready. Make sure all Pods are ready before trying to connect, otherwise you might get unexpected errors. To check that all Kubeflow-related Pods are ready, use the following commands:

```
kubectl get pods -n cert-manager
kubectl get pods -n istio-system
kubectl get pods -n auth
kubectl get pods -n knative-eventing
kubectl get pods -n knative-serving
kubectl get pods -n kubeflow
kubectl get pods -n kubeflow-user-example-com
# Depending on your installation if you installed KServe
kubectl get pods -n kserve
```


### To get started quickly, you can access Kubeflow via port-forward. Run the following to port-forward Istio’s Ingress-Gateway to local port 8080:
```
kubectl port-forward svc/istio-ingressgateway -n istio-system 8080:80
```

After running the command, you can access the Kubeflow Central Dashboard by doing the following:
```
http://localhost:8080
```

> username: user@example.com
> password: 12341234
