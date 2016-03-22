## Surfline Model Data Extraction, Transformation, Loading and Management

[Luigi](https://github.com/spotify/luigi) scripts for model data ETL and job management.

#### Design
This project is designed by 
* utilizing Luigi for AWS job workflow control and management
* making the parameters configurable as far as possible 

#### Deployment Dependencies

You need several Python libraries deployed to run the Luigi work. 
As part of deployment process, Jenkins job should handle this deployment during bootstrapping. 

* [Luigi](https://github.com/spotify/luigi): Workflow management
* [boto](https://github.com/boto/boto): Interface to Amazon Web Services

#### Deploying to AWS EMR cluster and Running on Spark

To deploy the Luigi scripts and related job, we setup a Jenkins job.
It will deploy the scripts from [science-data-extraction repo](https://github.com/Surfline/science-data-extraction)
to the dedicated AWS EMR cluster. It will also deploy the relevant configuration files. 

Once the scripts and configuration files are deployed, you can run ETL process with the `wf_spark_etl.py` Luigi script.
 
**For example:**
 
run the following will take in the parameters from the file `LUIGI_CONFIG_PATH`, invoke `wf_spark_etl.py` with the class `ModelCheckAndProcess` and submit the PySpark `app-file` with additional arguments `app-opts`. 

`export LUIGI_CONFIG_PATH=<Path to config file>;export TIME_TAG=$(date +%s); python wf_spark_etl.py ModelCheckAndProcess --app-file <Python app file> --app-opts "<Python app arguments>" --time-tag $TIME_TAG`
  
  * `LUIGI_CONFIG_PATH=<Path to config file>`: store all configuration. Samples config files in this repo:
  	- `bestwind_local.cfg`: configuration to run the job locally
  	- `bestwind_aws.cfg`: configuration to run the job in AWS EMR
  * `TIME_TAG`: obtain current time for tracking and task differentiation
  * `--app-file <Python app file>`: set Python file to `<Python app file>` to submit with Spark
  * `--app-opts "<Python app arguments>"`: set options with submitted Python file 

**Concrete example (replace the values for your own settings)**

`export LUIGI_CONFIG_PATH=/opt/science-data-extraction/bestwind_local.cfg; export TIME_TAG=$(date +%s); python wf_spark_etl.py ModelCheckAndProcess --app-file /opt/science-data-extraction/SparkExtract.py --app-opts "--s3_data xxx --s3_date yyy" --time-tag $TIME_TAG`
#### Eclipse Setup (WIP)

To import this project into Eclipse, you will need...
