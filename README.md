# Chicken Disease Project

**Note:**Implementations of end-to-end deep learning project

## Steps

* create and activate the environment
```bash
conda create -n dl-env python=3.8 -y
conda activate dl-env
```

* create template.py to add folder structure
```bash
touch template.py
```

* define a setup.py file

* add required libraries to requirements.txt and pip install it
```bash
pip freeze
pip freeze | grep pandas
```
**Note:** The **Logging** is a means of tracking events that happen when some software runs. 
*  add code to src/cnnClassifier/__init__.py  to define logging and create test.py for test purpose

**Note:** The **utils.py** makes it easy to execute common tasks in Python scripts
* define utils (src/cnnClassifier/utils/utils.py)

```
### Workflows
1. Update config.yaml
2. Update secrets.yaml [Optional]
3. Update params.yaml
4. Update the entity
5. Update the configuration manager in src config
6. Update the components
7. Update the pipeline
8. Update the main.py
9. Update the dvc.yaml
```


###########**Data Ingestion Section**##############

* [Data-Link](https://github.com/FraidoonOmarzai/data/blob/main/Chicken_disease_img.zip)
* first we will run on jupyter-notebook
* add code to config.yaml ---> constants/__init__.py ---> create research/01_data_ingestion.ipynb and run it
* create entity/config_entity.py ---> configuration.py ---> components/data_ingestion.py ---> pipeline/stage_01_data_ingestion.py ---> and define main.py and run **python main.py**



###########**Prepare Base Model Section**###########

**Note:** **Static methods** in Python are extremely similar to python class level methods, the difference being that a static method is bound to a class rather than the objects for that class. This means that a static method can be called without an object for that class.

* Define a config/config.yaml and params.yaml ---> Create research/02_prepare_base_model.ipynb and run it
* define entity/config_entity.py ---> config/configuration.py ---> components/prepare_base_model.py (create) ---> pipeline/stage_02_prepare_base_model.py (create) ---> define main.py



###########**Prepare Callbacks Section**############

* Define config/config.yaml ---> create research/03_prepare_callbacks.ipynb and run it
* create components/prepare_callbacks.py ---> config/configuration.py ---> entity/config_entity.py



###########**Training Section**####################

* Define a config/config.yaml ---> Create research/04_training.ipynb and run it
* define entity/config_entity.py ---> config/configuration.py ---> components/training.py (create) ---> pipeline/stage_03_training.py (create) ---> define main.py

###########**Evaluation Section**##################

* Create research/05_evaluation.ipynb and run it
* define entity/config_entity.py ---> config/configuration.py ---> components/evaluation.py (create) ---> pipeline/stage_04_evaluation.py (create) ---> define main.py


#############**DVC Section**######################

* add code to dvc.yaml and run the below commands
```bash
dvc init
dvc repro
dvc dag
```

#############**app Section**######################

* define index.html
* create function pipeline/prediction.py
* create app.py and define it


###############**Dockerfile and cicd Section**################

* create Dockerfile
```bash
FROM python:3.8-slim-buster

RUN apt update -y && apt install awscli -y
WORKDIR /app

COPY . /app
RUN pip install -r requirements.txt

CMD ["python3", "app.py"]
```

* create .github/workflows/cicd.yaml



******************************************************************************************************

###############**AWS Section**################

**Note:** we will deploy AWS-CICD using Github-Actions

### 1. Login to AWS console
### 2. Create IAM user for deployment and download the chicke-project_accessKeys
```bash
#with specific access

1. ECR: Elastic Container registry to save your docker image in aws
2. EC2 access : It is virtual machine


#Description: About the deployment

1. Build docker image of the source code

2. Push your docker image to ECR

3. Launch Your EC2 

4. Pull Your image from ECR in EC2

5. Lauch your docker image in EC2

#Policy for IAM:

1. AmazonEC2ContainerRegistryFullAccess
2. AmazonEC2FullAccess
```

### 3. Create ECR repo to store/save docker image
```bash
- Save the URI: 060145207853.dkr.ecr.ap-south-1.amazonaws.com/chicke-project
```

### 4. Create EC2 machine (Ubuntu)
### 5. Open EC2 and Install docker in EC2 Machine:
```bash
#optinal

sudo apt-get update

sudo apt-get upgrade -y

#required

curl -fsSL https://get.docker.com -o get-docker.sh

sudo sh get-docker.sh

sudo usermod -aG docker ubuntu

newgrp docker
```
### 6. Configure EC2 as self-hosted runner:
```bash
setting-->actions-->runner-->new self hosted runner--> choose os--> copy each command and run it on EC2 Instance Connect
```
### 7. Setup github secrets:
```bash
AWS_ACCESS_KEY_ID=

AWS_SECRET_ACCESS_KEY=

AWS_REGION = ap-south-1

AWS_ECR_LOGIN_URI = demo>>  060145207853.dkr.ecr.ap-south-1.amazonaws.com

ECR_REPOSITORY_NAME = chicke-project
```
******************************************************************************************************