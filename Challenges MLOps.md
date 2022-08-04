### Challenges of deployment of machine learning models on the production
 1- Change in data (Data drift)
 2- It takes more than model development it self

### The requirement surrounding ML infrustructure
![Alt text](/images/mlinfrusturcture.png)


### Problems a model may face after deployment:
  * Concept drift
    - Change in the outputs of the data (Y)
  * Data drift
    - Change in the input data (X)
   
There are two types of change:
  * Gradual changes (Some new words maybe added to a language through time)
  * Sudden changes (A new phone has a new microphone and the input data is completely changed)
  Important task => Manage the changes to the data
  
### Software engineering issues
  * Realtime or batch process?
  * Cloud or edge/browser?
  * Computing resources
  * Latency/Throughput (QPS)
  * Logging
  * Security and privacy


### First deployment vs Maintenance deployment


### Deployment patterns:
  * _Canary deployment_:
    Only partially send the data to models
  * _Blue Green deployment_:
    Have both old(blue) and new(green) system in the production environment and switch between them suddenly
  * _Degree of automation_:
      ![Alt text](/images/deploymentlevel.png)

