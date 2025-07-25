# Importing required libraries 
import requests  # For making API requests
import json      # For parsing JSON data

# Function to convert currency
def convert_currency(amount, from_currency, to_currency):

# API Key
    API_KEY = 'a1b87b34eeea1785b4b512bb'  # Replace with your actual key

# API endpoint URL formatted with the given currency and API key
    url = f"https://v6.exchangerate-api.com/v6/{API_KEY}/latest/{from_currency.upper()}"

# Sending GET request to the API
    response = requests.get(url)

# Parsing the JSON response
    data = response.json()

# Check for valid response and data
    if response.status_code != 200 or "conversion_rates" not in data:
        print("Error fetching exchange rates.")
        return

# Extract the exchange rates dictionary
    rates = data['conversion_rates']
    
# check if target currency is available
    if to_currency.upper() not in rates:
        print(f"Currency {to_currency.upper()} not found.")
        return

# Get exchange rate and calculate converted amount
    exchange_rate = rates[to_currency.upper()]
    converted_amount = round(amount * exchange_rate, 2) # Rounded to 2 decimal places

# Display the result
    print(f"\n💱 {amount} {from_currency.upper()} = {converted_amount} {to_currency.upper()}")
    print(f"(Exchange rate: 1 {from_currency.upper()} = {exchange_rate} {to_currency.upper()})")

# Main CLI code

# Ask user for amount to convert
amount = float(input("Enter amount: "))

# Ask user for source currency code (e.g., USD)
from_currency = input("From currency (e.g., USD): ")

# Ask user for target currency code (e.g., INR)
to_currency = input("To currency (e.g., INR): ")

# Call the function to perform conversion.
convert_currency(amount, from_currency, to_currency)


