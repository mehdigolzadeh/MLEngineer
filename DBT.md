Create venv

```
python3 -m venv <virtual-environment-name>
source name/bin/activate
```


c:\Telenet\DBT>activate dbtconda
```
dbt debug
dbt run
```

# DBT resouces
| Resource  | Description  |
|---|---|
| models  | Each model lives in a single file and contains logic that either transforms raw data into a dataset that is ready for analytics or, more often, is an intermediate step in such a transformation.  |
| snapshots  | A way to capture the state of your mutable tables so you can refer to it later.  |
| seeds  | CSV files with static data that you can load into your data platform with dbt.  |
| data tests | SQL queries that you can write to test the models and resources in your project. |
| macros	| Blocks of code that you can reuse multiple times. |
| docs	| Docs for your project that you can build. |
| sources	| A way to name and describe the data loaded into your warehouse by your Extract and Load tools. |
| exposures	| A way to define and describe a downstream use of your project. |
| metrics	| A way for you to define metrics for your project. |
| groups	| Groups enable collaborative node organization in restricted collections. |
| analysis	| A way to organize analytical SQL queries in your project such as the general ledger from your QuickBooks. |



# AIRFLOW

```
pip install apache-airflow
airflow initdb
airflow webserver -p portnum
```

https://www.youtube.com/watch?v=CLUhL6-RpqU
