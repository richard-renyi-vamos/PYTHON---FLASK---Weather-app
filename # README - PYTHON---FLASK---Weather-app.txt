CLAUDE.AI CONVERSATION

------------


create a PYTHON WEB APP that shows the temperature at a set location

Edit
Here's a simple Python web app using Flask that shows the temperature at a set location:

python

Copy
from flask import Flask, render_template
import requests

app = Flask(__name__)

# OpenWeatherMap API key and location
API_KEY = "YOUR_API_KEY_HERE"
CITY = "London,UK"

@app.route('/')
def get_temperature():
    base_url = "http://api.openweathermap.org/data/2.5/weather"
    params = {
        "q": CITY,
        "appid": API_KEY,
        "units": "metric"  # Use Celsius
    }
    
    response = requests.get(base_url, params=params)
    data = response.json()
    
    if response.status_code == 200:
        temperature = data['main']['temp']
        return render_template('temperature.html', city=CITY, temperature=temperature)
    else:
        return f"Error: Unable to fetch temperature data. Status code: {response.status_code}"

if __name__ == '__main__':
    app.run(debug=True)
