aws configure sso
setx AWS_PROFILE features-de-prod
aws sts get-caller-identity
aws configure set default.profile features-de-prod

aws s3 cp /path/to/extracted-data.csv s3://your-migration-bucket-name/
aws s3 sync s3://my-source-bucket s3://my-destination-bucket to copy the bucket data


to sync oracle tables with s3

*First import job:*
```
warp run -e prod --deployed --stream-name "mailboxImport" --spark-args "--conf spark.executor.instances=1 --conf spark.driver.memory=6g --conf spark.executor.memory=6g --class be.telenet.bdp.datalake.spss.ci.pilot.mcgyver.job.SpssCarImportJob" --app-args "-s mailboxImport -d 2023/07"
```
*Then prepare job:*
```
warp run -e prod --deployed --stream-name "mailbox" --spark-args "--conf spark.executor.instances=1 --conf spark.driver.memory=6g --conf spark.executor.memory=6g --class be.telenet.bdp.datalake.spss.ci.pilot.mcgyver.job.SpssCarPrepareJob" --app-args "-s mailbox -d 2023/06"
```
