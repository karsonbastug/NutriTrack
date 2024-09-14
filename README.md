# NutriTrack Dashboard - Screenshot
<img width="1025" alt="image" src="https://github.com/user-attachments/assets/1839ddec-8a26-48f9-8266-9d606de62bbb">

## With Specific Food Selected

<img width="1009" alt="image" src="https://github.com/user-attachments/assets/ac6ce3c0-8d67-4db5-927e-34adab43c70c">



# Purpose
The purpose of this project was to create a simplified way to keep track of your diet intake. By minimizing the input needed as a user, it encourages more frequent tracking of foods consumed, promoting your health.

# Functionality
The dhasboard utilizes NutritionX's food API to query the nutritional information. This API is called upon in Google Collab using Python code - users type in the food they consumed, and the API (nutrition information for that food) is called and stored in a published google sheet. This sheet is where the Power BI pulls its data from.

# Design
Originally, the Power BI was intended to utilize the REST API directly within the report to minimize the need of a third party. However, as of September 2024, Power BI does not currently support the historical storing of API results. As such, the data needs to be stored and the API called elsewhere. 

# Google Collab Code
Within this repository is the Python code being utilized in Google Collab. If you wish to use this code for your own report, you must retreieve your own API key and ID from NutritionX. Up to two keys/IDs can be obtained and used for free.

[Link to signup](https://www.nutritionix.com/business/api)

When you sign up, you will be prompted with the API key, ID, and documentaiton. Once you run the code, you will be ready to copy the Web link for the Google Sheet to Power BI to be utilized.

Have fun!




