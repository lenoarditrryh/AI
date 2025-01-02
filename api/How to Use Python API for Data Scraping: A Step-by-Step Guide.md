
# How to Use Python API for Data Scraping: A Step-by-Step Guide

## Introduction

This article is a technical tutorial focused on sharing knowledge for educational purposes. It does not involve any commercial activities, piracy, or unethical practices. 

*If there are any issues regarding infringement, please contact the author.*

In this guide, we’ll show you how to use Python to scrape data using APIs, particularly focusing on scraping daily bestseller rankings with up to 1,500 top-selling products.

---

## Step 1: Obtain an Access Token for API Authentication

Before starting, ensure you have the appropriate user permissions. If you're only a **basic user**, this method may not work as advanced permissions are often required. For this example, we’ll be using an account with premium-level access.

### Libraries Required

Install the following Python libraries if you haven't already:

```bash
pip install requests hashlib
```

### How to Obtain the Access Token

To scrape data, you'll need to log in and obtain an access token. Follow these steps:

1. **Inspect HTTP Requests**: Open your browser's developer tools (F12) and navigate to the `Network` tab. Select `Fetch/XHR` and log in to the platform. This allows you to view the HTTP requests made during login.
2. **Copy Request Headers**: Select a network request and copy the request headers.

Here’s how the Python script for the login process looks:

```python
import requests
import hashlib

# Encrypt the password using MD5
password = "your_password"
md5_hash = hashlib.md5()
md5_hash.update(password.encode())
hex_digest = md5_hash.hexdigest()

# Login payload
json_data = {
    'from_platform': None,
    'appId': 10000,
    'timeStamp': 1681976003,  # Replace with the correct timestamp
    'username': 'your_username',
    'password': hex_digest
}

# Add the required headers
headers = {
    'User-Agent': 'Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/107.0.0.0 Safari/537.36',
    'Content-Type': 'application/json'
}

# Send the login request
response = requests.post('https://api-service.chanmama.com/v1/access/token', headers=headers, json=json_data)
rsp = response.json()
print(rsp)

# Extract the token from the response
access_token = rsp['data']['token']
```

Verify that the `access_token` field exists in the response. This token will be used for subsequent requests.

---

## Step 2: Extract Bestseller Data Using API Requests

### Analyze API Endpoints

To find the correct API endpoint for bestseller data:
1. Open the browser's developer tools and monitor network requests.
2. Navigate to the section of the platform where bestseller data is displayed.
3. Identify the API endpoint URL, which often includes query parameters like `rank` or `category`.

For example:
```plaintext
https://api-service.chanmama.com/v6/home/rank/yesterdaySaleRank
```

### Parameters for API Requests

Below is the Python code to send a request to the API:

```python
url = 'https://api-service.chanmama.com/v6/home/rank/yesterdaySaleRank'

# Pass the access token in cookies
cookies = {
    'LOGIN-TOKEN-FORSNS': access_token,
}

# Add the required headers
headers = {
    'authority': 'api-service.chanmama.com',
    'accept': 'application/json, text/plain, */*',
    'user-agent': 'Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/107.0.0.0 Safari/537.36',
}

# Customize query parameters
params = {
    'platform': 'jinritemai',
    'date': '2023-12-31',  # Replace with the desired date
    'day_type': 'day',
    'big_promotion': '0',
    'page': 1,
    'size': 100,
    'sort': 'volume',
    'category_id': '14',  # Replace with the desired category ID
}

# Send the request
response = requests.get(url, params=params, cookies=cookies, headers=headers)
rsp = response.json()
print(rsp)
```

### Dealing with Encrypted Data

If the response data is encrypted, you’ll need to decrypt it. Search GitHub for decryption solutions or consult with developers for specific libraries or techniques.

---

## Example Workflow Recap

1. **Login to Obtain Token**: Use the login API to obtain the `access_token` required for authentication.
2. **Inspect Network Requests**: Identify the relevant API endpoint and query parameters.
3. **Send Requests**: Use Python's `requests` library to send authenticated requests and fetch data.
4. **Handle Responses**: Process the JSON response to extract the desired information.

---

## Key Considerations for Data Scraping

- **Ethical Usage**: Ensure you have permission to scrape data and comply with the platform's terms of service.
- **Data Privacy**: Abide by data protection laws such as GDPR when collecting or using customer data.
- **Error Handling**: Implement error-handling mechanisms in your script to manage issues like invalid tokens, rate limits, or data encryption.

---

## Simplify Data Scraping With ScraperAPI

Stop wasting time dealing with proxies and CAPTCHAs! ScraperAPI is an efficient tool that handles millions of web scraping requests for you. Focus on the data instead of worrying about complex setups.

### Why Choose ScraperAPI?

- **Handles Proxies & CAPTCHAs**: ScraperAPI manages all backend complexities.
- **Supports Structured Data**: Scrape JSON from popular platforms like Amazon, Google, and Walmart.
- **Free Trial Available**: Start scraping today with 5,000 free API credits.

[👉 Start Your Free Trial Now!](https://www.scraperapi.com/?fp_ref=coupons)

---

By following this guide, you can effectively scrape data using Python APIs and enhance your workflow with tools like ScraperAPI. Happy coding!
