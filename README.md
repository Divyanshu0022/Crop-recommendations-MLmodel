# AutoAI Crop Recommendation System using IBM watsonx.ai
<img width="1920" height="1080" alt="Screenshot (296)" src="https://github.com/user-attachments/assets/54087f09-5c33-48a2-8af6-904321a50f62" />
<img width="1920" height="1080" alt="Screenshot (297)" src="https://github.com/user-attachments/assets/0b8bbe36-fa7e-46d8-8c9c-9494683e5584" />

This project demonstrates the use of **IBM's AutoAI capabilities** within the `watsonx.ai Studio` to build, deploy, and test a machine learning model for crop recommendation. The model predicts the most suitable crop to grow based on various environmental and soil parameters, aiming to maximize agricultural yield through precision agriculture. 

This guide provides a detailed walkthrough of the entire process, from setting up the IBM Cloud environment to testing the final deployed model.

## 📖 About the Dataset

The model is trained on a comprehensive dataset created by augmenting rainfall, climate, and fertilizer data from India. [cite: 8] The dataset contains the following features:
* **N**: Ratio of Nitrogen content in the soil 
* **P**: Ratio of Phosphorous content in the soil 
* **K**: Ratio of Potassium content in the soil 
* **temperature**: Temperature in degrees Celsius 
* **humidity**: Relative humidity in % 
* **ph**: pH value of the soil 
* **rainfall**: Rainfall in mm 
* **label**: The target crop name (the column to be predicted)

## 🛠️ Platform and Services Used
* **IBM Cloud**: The cloud platform hosting all services.
* **watsonx.ai Studio**: An integrated environment for data science and machine learning tasks.
* **AutoAI Experiment**: An automated tool that simplifies and accelerates the ML model-building process.
* **Cloud Object Storage**: Used to store the project assets, including the dataset.
* **watsonx.ai Runtime**: The compute service required to run the AutoAI experiment and deploy the model.

---

## 🚀 Step-by-Step Project Workflow

Here is the detailed process followed to create and deploy the crop recommendation model.

### **Step 1: Login to IBM Cloud**
Begin by logging into your **IBM Cloud account**. 

### **Step 2: Clean Up Resources**
To prevent conflicts and ensure a smooth setup, it's a good practice to first delete any existing services or resources in your resource list that you no longer need. 

### **Step 3: Create a watsonx.ai Studio Project**
1.  Navigate to the IBM Cloud catalog and search for **`watsonx.ai Studio`**. 
2.  Create a new `watsonx.ai Studio` service. For this project, a **`watsonx.ai Runtime`** is essential for computation.
3.  Create a new project and configure it by adding a **Cloud Object Storage** service for data storage. 
4.  Specify the hardware resources for the runtime environment. For this project, a configuration of **8 CPU and 32 GB RAM** was used, which consumes **20 CUH (Capacity Units per Hour)**.

    > **What are CUH?** Capacity Unit Hours (CUH) are the units used by IBM to measure the consumption of processing power for services like AutoAI and model training.

### **Step 4: Add the Dataset**
Once the project is set up, create a new AutoAI experiment.In the experiment, upload the `Crop_Recommendation.csv` dataset from your local machine. 

### **Step 5: Select the Prediction Field**
After the dataset is loaded, configure the experiment by specifying what the model should predict. For this project, the **`label`** column (which contains the crop name) was selected as the prediction target. 

### **Step 6: Run the AutoAI Experiment**
With the configuration set, **run the experiment**. 

> **What happens during an AutoAI experiment?** The `watsonx.ai` service automates several key machine learning steps:
> * **Data Preprocessing**: Cleaning and preparing the data for training.
> * **Feature Engineering**: Creating new, informative features from the existing data.
> * **Model Selection**: Testing various algorithms (like Logistic Regression, Random Forest, LGBM Classifier, etc.) to find the best fit. 
> * **Hyperparameter Optimization**: Fine-tuning the best-performing model to enhance its accuracy.
>
> The experiment generates multiple **pipelines**, each representing a unique combination of these steps. 

### **Step 7: Select and Save the Best Pipeline**
After the experiment completes, review the **Pipeline Leaderboard**, which ranks all the generated models by a chosen metric (e.g., Accuracy).  Select the pipeline with the highest accuracy—in this case, **Pipeline 2 (LGBM Classifier)**—and save it as a model asset. 

### **Step 8: Promote the Model to a Deployment Space**
To make the model usable, it must be moved to a production environment.
1.  **Promote** the saved model to a **Deployment Space**. 
2.  If you don't have one, create a new deployment space and associate the **`watsonx.ai Runtime`** service with it. 

> **What is a Deployment Space?** It's a dedicated environment where you can manage, deploy, and monitor your machine learning models to make them available for applications.

### **Step 9: Deploy the Model**
Within the deployment space, create a **New deployment** for the model. [ Select the **`Online`** deployment type, which makes the model available to accept data and return predictions in real-time.

### **Step 10: Test the Deployed Model**
Finally, test the live model:
1.  Navigate to the **Test** tab of your deployment. 
2.  Enter new input values for N, P, K, temperature, humidity, pH, and rainfall either manually or using a JSON input. 
3.  Click **Predict**. The model will return the predicted crop name along with a confidence score, showing how certain it is about the prediction. 

For example, the model successfully predicted **chickpea** with a **99% confidence** based on the provided test data. 

---
