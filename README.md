# mlflow Demonstration

This repo demonstrates the use of the open source project [mlflow](https://mlflow.org), which is used to record 
and manage results of machine learning experiments.  Docker containers
provide the run-time environment for this demonstration.

Code used in this demonstration is based on these mflow examples: 
[`examples/sklearn_elasticnet_wine`](https://github.com/mlflow/mlflow/tree/master/examples/sklearn_elasticnet_wine) 
and [`examples/r_wine`](https://github.com/mlflow/mlflow/tree/master/examples/r_wine)

## Demonstration Environment
![](images/demo_environment_architecture.png)


## System Requirements
* [Docker](https://docs.docker.com/develop/)
* [Docker Compose](https://docs.docker.com/compose/overview/)

Work performed with Docker for Mac Version 2.0.0.3 (31259)


## Initial Setup
* Clone repo to local computer.  Note directory for the local repo, e.g., `/home/userid/mlflow_demo`
* Create directory to hold mlflow server tracking data and artifacts, e.g., `/home/userid/mlflow_server`.  Within this  
directory create two subdirectories called `tracking` and `artifacts`
```
/home/userid/mlflow_server/tracking
/home/userid/mlflow_server/artifacts
```
* Change working directory to `run_demo`
* Update contents of `./setup_environment_variables` to specify values for three required environment variables. 
If required specify version of mlflow package.  See example below.
```
# version of mlflow to install in containers
export MLFLOW_VERSION=0.8.2

# directory containing demonstration source code
export MLFLOW_DEMO_DIRECTORY=/home/userid/mlflow_demo

# directory to hold mlflow tracking and artifacts
export MLFLOW_TRACKING_DIRECTORY=/home/userid/mlflow_server

```
* After updating `setup_environment_variables`, execute following command to set  
environment variables: `. ./setup_environment_variables`

* Run the following command to initially build the required Docker images.
```
bash ./build_images
```
Note:  On a MacbookPro with 16GB RAM, it took about 13 minutes for the initial 
build of the three images.


## Start demonstration containers
After building the three Docker images, navigate to `./run_demo`.   Ensure the three required
environment variables are defined by running `. ./setup_environment_variables`.
* To bring up the three containers:
```
docker-compose up --detach
```
* To stop the three containers:
```
docker-compose down
```

## Connecting to containers
Open a browser and enter the following URL for the respective service.
* Python Container:  `http://0.0.0.0:8888`
* R Container: `http://0.0.0.0:8787`
* mlflow tracking server: `http://0.0.0.0:5000`