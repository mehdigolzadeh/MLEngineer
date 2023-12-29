# Deploy models:

[Initial info about the model deployment](https://docs.aws.amazon.com/sagemaker/latest/dg/deploy-model.html)


# Deploy on an live inference endpoint

```
# cell 14
xgb_predictor = xgb.deploy(initial_instance_count=1,
                           instance_type='ml.m4.xlarge')

# cell 15
xgb_predictor.serializer = sagemaker.serializers.CSVSerializer()

# cell 16
def predict(data, predictor, rows=500 ):
    split_array = np.array_split(data, int(data.shape[0] / float(rows) + 1))
    predictions = ''
    for array in split_array:
        predictions = ','.join([predictions, predictor.predict(array).decode('utf-8')])

    return np.fromstring(predictions[1:], sep=',')

predictions = predict(test_data.drop(['y_no', 'y_yes'], axis=1).to_numpy(), xgb_predictor)

# cell 17
pd.crosstab(index=test_data['y_yes'], columns=np.round(predictions), rownames=['actuals'], colnames=['predictions'])
```
## Delete the endpoint
```
xgb_predictor.delete_endpoint(delete_endpoint_config=True)
```

# Serverless deployment

```
# Setup clients
import boto3

client = boto3.client(service_name="sagemaker")
runtime = boto3.client(service_name="sagemaker-runtime")

# Retrieve model data from training job
model_artifacts = xgb.model_data
model_artifacts
```
### Model Creation
Create a model by providing your model artifacts, the container image URI, environment variables for the container (if applicable), a model name, and the SageMaker IAM role.
```
from time import gmtime, strftime

model_name = "xgboost-serverless" + strftime("%Y-%m-%d-%H-%M-%S", gmtime())
print("Model name: " + model_name)

# dummy environment variables
byo_container_env_vars = {"SAGEMAKER_CONTAINER_LOG_LEVEL": "20", "SOME_ENV_VAR": "myEnvVar"}

create_model_response = client.create_model(
    ModelName=model_name,
    Containers=[
        {
            "Image": container,
            "Mode": "SingleModel",
            "ModelDataUrl": model_artifacts,
            "Environment": byo_container_env_vars,
        }
    ],
    ExecutionRoleArn=role,
)

print("Model Arn: " + create_model_response["ModelArn"])
```

### Endpoint Configuration Creation
This is where you can adjust the Serverless Configuration for your endpoint. The current max concurrent invocations for a single endpoint, known as MaxConcurrency, can be any value from 1 to 200, and MemorySize can be any of the following: 1024 MB, 2048 MB, 3072 MB, 4096 MB, 5120 MB, or 6144 MB.

```
xgboost_epc_name = "xgboost-serverless-epc" + strftime("%Y-%m-%d-%H-%M-%S", gmtime())

endpoint_config_response = client.create_endpoint_config(
    EndpointConfigName=xgboost_epc_name,
    ProductionVariants=[
        {
            "VariantName": "byoVariant",
            "ModelName": model_name,
            "ServerlessConfig": {
                "MemorySizeInMB": 4096,
                "MaxConcurrency": 1,
            },
        },
    ],
)

print("Endpoint Configuration Arn: " + endpoint_config_response["EndpointConfigArn"])
```

### Serverless Endpoint Creation
Now that we have an endpoint configuration, we can create a serverless endpoint and deploy our model to it. When creating the endpoint, provide the name of your endpoint configuration and a name for the new endpoint.

```
endpoint_name = "xgboost-serverless-ep" + strftime("%Y-%m-%d-%H-%M-%S", gmtime())

create_endpoint_response = client.create_endpoint(
    EndpointName=endpoint_name,
    EndpointConfigName=xgboost_epc_name,
)

print("Endpoint Arn: " + create_endpoint_response["EndpointArn"])


# wait for endpoint to reach a terminal state (InService) using describe endpoint
import time

describe_endpoint_response = client.describe_endpoint(EndpointName=endpoint_name)

while describe_endpoint_response["EndpointStatus"] == "Creating":
    describe_endpoint_response = client.describe_endpoint(EndpointName=endpoint_name)
    print(describe_endpoint_response["EndpointStatus"])
    time.sleep(15)

describe_endpoint_response
```

### Endpoint Invocation
Invoke the endpoint by sending a request to it. The following is a sample data point grabbed from the Direct Marketing dataset.
```
payload = b"3., 999.,   0.,   1.,   0.,   0.,   0.,   0.,   0.,   0.,   0., 1.,   0.,   0.,   0.,   0.,   0.,   1.,   0.,   0.,   0.,   0., 0.,   0.,   0.,   0.,   0.,   1.,   0.,   1.,   0.,   0.,   1., 0.,   0.,   1.,   0.,   0.,   1.,   0.,   0.,   0.,   0.,   1., 0.,   0.,   0.,   0.,   0.,   0.,   0.,   1.,   0.,   0.,   0., 0.,   1.,   0."

response = runtime.invoke_endpoint(
    EndpointName=endpoint_name,
    Body=payload,
    ContentType="text/csv",
)

print(response["Body"].read().decode())
```

### Clean Up
Delete any resources you created in this notebook that you no longer wish to use.

```
client.delete_model(ModelName=model_name)
client.delete_endpoint_config(EndpointConfigName=xgboost_epc_name)
client.delete_endpoint(EndpointName=endpoint_name)
```
