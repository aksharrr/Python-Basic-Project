# weather-dashboard.py
import requests
import matplotlib.pyplot as plt

class WeatherAPI:
    def __init__(self, api_key):
        self.api_key = api_key
        self.base_url = "https://api.openweathermap.org/data/2.5/weather"

  def get_weather(self, city):
        try:
            response = requests.get(
                self.base_url,
                params={"q": city, "appid": self.api_key, "units": "metric"}
            )
            response.raise_for_status()
            return response.json()
        except requests.exceptions.RequestException as e:
            print(f"Error: {e}")
            return None

class WeatherDashboard:
    def __init__(self, api):
        self.api = api

  def display_weather(self, city):
        data = self.api.get_weather(city)
        if data:
            temp = data["main"]["temp"]
            humidity = data["main"]["humidity"]
            description = data["weather"][0]["description"]
        print(f"City: {city}")
            print(f"Temperature: {temp}°C")
            print(f"Humidity: {humidity}%")
            print(f"Description: {description.capitalize()}")

self.plot_weather([temp, humidity])

def plot_weather(self, data):
        labels = ["Temperature (°C)", "Humidity (%)"]
        plt.bar(labels, data, color=['blue', 'orange'])
        plt.title("Weather Data")
        plt.show()

if __name__ == "__main__":
    api_key = "YOUR_API_KEY"  # Replace with your OpenWeatherMap API key
    api = WeatherAPI(api_key)
    dashboard = WeatherDashboard(api)
  city = input("Enter the city: ")
    dashboard.display_weather(city)
