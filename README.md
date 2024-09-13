# NutriTrack Dashboard - Screenshot
<img width="959" alt="Dashboard" src="https://github.com/user-attachments/assets/c47b904d-c2e0-4fa1-bc7d-982f2abf5b95">


# Purpose
The purpose of this project was to create a simplified way to keep track of your diet intake. By minimizing the input needed as a user, it encourages more frequent tracking of foods consumed, promoting your health.

# Functionality
The dhasboard utilizes NutritionX's food API to query the nutritional information. This API is called upon in Google Collab using Python code - users type in the food they consumed, and the API (nutrition information for that food) is called and stored in a published google sheet. This sheet is where the Power BI pulls its data from.

# Design
Originally, the Power BI was intended to utilize the REST API directly within the report to minimize the need of a third party. However, as of September 2024, Power BI does not currently support the historical storing of API results. As such, the data needs to be stored and the API called elsewhere. 

## Google Collab Code
Below is the Python code being utilized in Google Collab. If you wish to use this code for your own report, you must retreieve your own API key and ID from NutritionX. Up to two keys/IDs can be obtained and used for free.

[Link to signup](https://www.nutritionix.com/business/api)

When you sign up, you will be prompted with the API key, ID, and documentaiton.

Once you run this code, you will be ready to copy the Web link to Power BI to be utilized.

Have fun!

```import requests
import pandas as pd
from google.colab import drive
import os
import ipywidgets as widgets
from IPython.display import display

drive.mount('/content/drive')

API_URL = "https://trackapi.nutritionix.com/v2/natural/nutrients"
APP_ID = "your ID here"
APP_KEY = "your key here"

food_query_input = widgets.Text(
    description='Food Query:',
    placeholder='Type the food here',
    style={'description_width': 'initial'}
)

submit_button = widgets.Button(description='Submit')

def on_button_click(b):
    food_query = food_query_input.value
    if not food_query:
        print("Please enter a food query.")
        return
      
    headers = {
        "x-app-id": APP_ID,
        "x-app-key": APP_KEY,
        "Content-Type": "application/json"
    }
    payload = {
        "query": food_query
    }

    response = requests.post(API_URL, headers=headers, json=payload)

    if response.status_code == 200:
        data = response.json()
        food_items = data.get('foods', [])
        new_data_df = pd.DataFrame(food_items)
        drive_path = '/content/drive/MyDrive/nutrition_data.xlsx'  

        if os.path.exists(drive_path):
            
            existing_df = pd.read_excel(drive_path)
    
            combined_df = pd.concat([existing_df, new_data_df], ignore_index=True)
        else:
         
            combined_df = new_data_df

       
        combined_df.to_excel(drive_path, index=False)

        print(f"Data has been successfully appended to {drive_path}")
    else:
        print(f"Failed to retrieve data: {response.status_code}")
        print(response.text)

submit_button.on_click(on_button_click)

display(food_query_input, submit_button)
```
