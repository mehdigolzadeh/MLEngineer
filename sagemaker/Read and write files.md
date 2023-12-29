# Write csv using pandas:
```
model_data.to_csv('s3://tln-purpose-data-saber-sybikg/car-build/Sagemakerdata/bankdata.csv', index=False)
```

# Read CSV using Boto3:
```
import boto3
import pandas as pd

# Initialize the S3 client
s3 = boto3.client('s3')

# Specify the bucket name and file key (path to the CSV file in the bucket)
bucket_name = 'tln-purpose-data-saber-sybikg'
file_key = 'car-build/Sagemakerdata/bankdata.csv'

# Define a function to read CSV from S3 and return a Pandas DataFrame
def read_csv_from_s3(bucket, key):
    # Load the CSV file from S3 into a Pandas DataFrame
    obj = s3.get_object(Bucket=bucket, Key=key)
    df = pd.read_csv(obj['Body'])
    return df

# Read the CSV file from S3 into a DataFrame
model_data = read_csv_from_s3(bucket_name, file_key)

# Display the DataFrame
print(model_data.head())
```
