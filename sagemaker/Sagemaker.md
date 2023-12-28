# How to setup Sagemaker:

[getting started with sagemaker](https://docs.aws.amazon.com/sagemaker/latest/dg/gs.html)

# Pricing

[all services](http://aws.amazon.com/sagemaker/pricing/)

# An Amazon SageMaker Domain consists of the following:

* An associated Amazon Elastic File System (Amazon EFS) volume
* A list of authorized users
* A variety of security, application, policy, and Amazon Virtual Private Cloud (Amazon VPC) configurations

# AutoML
[how to create autoML models](https://docs.aws.amazon.com/sagemaker/latest/dg/autopilot-automate-model-development.html)

# All types of Sagemaker development environment
 * **Amazon SageMaker Studio:** The latest web-based experience for running ML workflows with a suite of IDEs. Studio supports the following applications.
      * Amazon SageMaker Studio Classic
      * Code Editor, based on Code-OSS, Visual Studio Code - Open Source
      * JupyterLab
      * Amazon SageMaker Canvas
      * RStudio
 * **Amazon SageMaker Studio Classic:** Lets you build, train, debug, deploy, and monitor your machine learning models.
 * **Amazon SageMaker Notebook Instances:** Lets you prepare and process data, and train and deploy machine learning models from a compute instance running the Jupyter Notebook application.
 * **Amazon SageMaker Studio Lab:** Studio Lab is a free service that gives you access to AWS compute resources, in an environment based on open-source JupyterLab, without requiring an AWS account.
 * **Amazon SageMaker Canvas:** Gives you the ability to use machine learning to generate predictions without needing to code.
 * **Amazon SageMaker geospatial:** Gives you the ability to build, train, and deploy geospatial models.
 * **RStudio on Amazon SageMaker:** RStudio is an IDE for R, with a console, syntax-highlighting editor that supports direct code execution, and tools for plotting, history, debugging and workspace management.
 * **SageMaker HyperPod:** SageMaker HyperPod lets you provision resilient clusters for running machine learning (ML) workloads and developing state-of-the-art models such as large language models (LLMs), diffusion models, and foundation models (FMs).


# Data preparation:
You can use Amazon **SageMaker Data Wrangler** to import, prepare, transform, visualize and analyze data. You can integrate Data Wrangler into your machine learning workflows to simplify and streamline data pre-processing and feature engineering using little to no coding. You can also add your own Python scripts and transformations to customize your data prep workflow.

After you have defined a data prep workflow or data flow, you can integrate it with **SageMaker Processing**, **SageMaker Pipelines**, and **SageMaker Feature Store**, simplify the task of processing, sharing, and storing ML training data. You can also export your data flow to a Python script and create a custom ML data prep pipeline.

For fast data preparation at scale, Amazon SageMaker Studio Classic provides a **built-in integration with Amazon EMR**. You can use SageMaker Studio Classic to connect to, provision, or manage Amazon EMR clusters from your notebook interface for petabyte-scale data processing, interactive analytics, and machine learning. Amazon EMR uses open-source frameworks such as Apache Spark, Apache Hive, or Presto. 

Alternatively, you can use the Apache Spark-based serverless engine from an **AWS Glue** interactive sessions to aggregate and transform data from multiple sources. You can aggregate and transform data from your analytics and ETL (extract, transform, and load) pipelines without needing to manage infrastructure.

You can use **Amazon SageMaker Clarify** to determine whether the data that you’re using to train models or your resulting model encodes any bias. SageMaker Clarify can also help you explain models created with tabular, image or NLP data with partial dependence plots, feature importance and more. For more information about SageMaker Clarify, see Detect Pre-training Data Bias.


# Example using EMR to process data 
[Example](https://sagemaker-examples.readthedocs.io/en/latest/sagemaker_processing/spark_distributed_data_processing/sagemaker-spark-processing.html)

[advanced scenario to build a processing container](https://docs.aws.amazon.com/sagemaker/latest/dg/build-your-own-processing-container.html)

