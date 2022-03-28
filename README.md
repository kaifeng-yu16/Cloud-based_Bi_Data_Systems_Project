# Drink_classification_Databricks_AutoML
[![CI with Github Actions](https://github.com/kaifeng-yu16/Cloud-based_Big_Data_Systems_Project/actions/workflows/main.yml/badge.svg)](https://github.com/kaifeng-yu16/Cloud-based_Big_Data_Systems_Project/actions/workflows/main.yml)

This is duke ids721 project3. This project trained a drink classification model using Databricks AutoML, serve it as a microservice using Flask, containerized it and deploy it to AWS App Runner.

## How to use
To use this app, go to website https://vimi8fhfnw.us-east-1.awsapprunner.com/predict/, enter "Volume", "Calories" and "Caffeine" info about your drink, and click "predict" to predict the type of your drink. Note, "Volume" could be a decimal number, "Calories" and "Caffeine" should be integers, and the result could be "Coffee", "Energy Drinks", "Energy Shots", "Soft Drinks", "Tea" or "Water".

![image](https://user-images.githubusercontent.com/90477174/160330039-5ee8b6bd-1558-42f3-8639-bb012e2f9727.png)

If you want to run this app locally, you can also pull the docker image from dockerhub:
```
docker pull kaifengyu16/drink_classification_container:v1
```
And then use the following command to run:
```
docker run kaifengyu16/drink_classification_container:v1
```

## Workflow
### Step 1: Preprocessing and Visualizing Dataset
The dataset for this project comes from Kaggle: [Caffeine Content of Drinks](https://www.kaggle.com/datasets/heitornunes/caffeine-content-of-drinks).

I use databricks code [preprocessing.ipynb](https://github.com/kaifeng-yu16/Cloud-based_Big_Data_Systems_Project/blob/main/preprocessing.ipynb) to preprocess data and visualize it.

The original dataset is [caffeine.csv](https://github.com/kaifeng-yu16/Cloud-based_Big_Data_Systems_Project/blob/main/caffeine.csv) and the preprocessed dataset is [caffeine_processed.csv](https://github.com/kaifeng-yu16/Cloud-based_Big_Data_Systems_Project/blob/main/caffeine_processed.csv) 

</br> 

### Step 2: Train Models
The models are trained using using Databricks AutoML and the best model is registered.

Model training process: [train_model.ipynb](https://github.com/kaifeng-yu16/Drink_classification_Databricks_AutoML/blob/main/train_model.ipynb)

To download the best model to local, first run [list_models.py](https://github.com/kaifeng-yu16/Cloud-based_Big_Data_Systems_Project/blob/main/list_models.py) and then change the model id in [download_model.py](https://github.com/kaifeng-yu16/Cloud-based_Big_Data_Systems_Project/blob/main/download_model.py) to download the model you desired. The downloaded model will be stored in directory [model/](https://github.com/kaifeng-yu16/Cloud-based_Big_Data_Systems_Project/tree/main/model). 
 
</br>

### Step 3: Serve the Model
The model is served as a microservice using Flask. Relavent code: [main.py](https://github.com/kaifeng-yu16/Cloud-based_Big_Data_Systems_Project/blob/main/main.py), [predict.html](https://github.com/kaifeng-yu16/Cloud-based_Big_Data_Systems_Project/tree/main/templates)
   
</br> 

### Step 4: Containerize and Deploy the microservice
Finally, I containerized the microservice and deploy it to AWS AppRunner.[How to deploy?](https://github.com/kaifeng-yu16/Containerized_microservice_deploy_AWS#aws-app-runner-deploy)
