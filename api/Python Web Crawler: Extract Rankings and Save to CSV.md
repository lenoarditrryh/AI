
# Python Web Crawler: Extract Rankings and Save to CSV

Learn how to build a Python web crawler to extract ranking data from an API and save the results into a CSV file. This tutorial walks you through the process step by step, providing code examples and helpful explanations.

---

Stop wasting time on proxies and CAPTCHAs! ScraperAPI's simple API handles millions of web scraping requests, so you can focus on the data. Get structured data from Amazon, Google, Walmart, and more. Start your free trial today! 👉 [https://www.scraperapi.com/?fp_ref=coupons](https://www.scraperapi.com/?fp_ref=coupons)

---

## Steps to Extract Rankings and Save to CSV

### Step 1: Find the API Endpoint

Open the webpage in your browser, press `F12` to open the developer tools, and locate the API endpoint used to fetch the rankings. Use tools like Postman to test and validate the API.

#### Example:
By analyzing the API, you’ll notice that adjusting parameters like `page`, `pageSize`, and `channel` in the request allows you to retrieve specific pages, the number of items per page, and the type of content.

### Step 2: Use a Loop to Extract Data

Using Python's `requests` library and a loop, you can automate data collection. The following code demonstrates how to extract titles, authors, views, and other information for the top 100 items.

```python
import requests
import csv

# Define headers for the API request
headers = {
    'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/95.0.4638.69 Safari/537.36'
}

# File path for saving the CSV file
csv_file_path = r'C:\Users\*****\Desktop\csdn_python_热榜.csv'

# Open a CSV file to write data
with open(csv_file_path, 'a', newline='') as f:
    csdn_data = csv.writer(f)
    csdn_data.writerow(['Article Title', 'Author', 'Views', 'Comments', 'Favorites', 'Heat Score', 'Article URL'])

    for i in range(0, 2):  # Loop through 2 pages (50 items per page)
        hot_rank_url = f'https://example-api-url?page={i}&pageSize=50&child_channel=python'
        res = requests.get(hot_rank_url, headers=headers)
        for a in range(0, 50):
            article = res.json()['data'][a]
            csv_message = [
                article.get('articleTitle', ''),
                article.get('nickName', ''),
                article.get('viewCount', ''),
                article.get('commentCount', ''),
                article.get('favorCount', ''),
                article.get('hotRankScore', ''),
                article.get('articleDetailUrl', '')
            ]
            csdn_data.writerow(csv_message)
```

### Step 3: Save Data to CSV

The data extracted from the API is saved to a CSV file. Each record includes information such as article title, author, views, comments, favorites, heat score, and URL.

#### Key Steps:
1. Append extracted data to a list.
2. Write the list to the CSV file using Python’s `csv` library.

---

## Full Code Example

Below is the complete code for scraping rankings and saving the results to a CSV file:

```python
import requests
import csv

# User-Agent header for API request
headers = {
    'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/95.0.4638.69 Safari/537.36'
}

# File path for saving the CSV file
csv_file_path = r'C:\Users\*****\Desktop\csdn_python_热榜.csv'

# Open the CSV file
with open(csv_file_path, 'a', newline='') as f:
    csdn_data = csv.writer(f)
    csdn_data.writerow(['Article Title', 'Author', 'Views', 'Comments', 'Favorites', 'Heat Score', 'Article URL'])

    for i in range(0, 2):  # Iterate through 2 pages
        hot_rank_url = f'https://example-api-url?page={i}&pageSize=50&child_channel=python'
        response = requests.get(hot_rank_url, headers=headers)

        for a in range(0, 50):  # Process 50 items per page
            data = response.json()['data'][a]
            article_title = data.get('articleTitle', '')
            author = data.get('nickName', '')
            views = data.get('viewCount', '')
            comments = data.get('commentCount', '')
            favorites = data.get('favorCount', '')
            heat_score = data.get('hotRankScore', '')
            article_url = data.get('articleDetailUrl', '')

            # Write to CSV
            csv_message = [article_title, author, views, comments, favorites, heat_score, article_url]
            csdn_data.writerow(csv_message)
```

---

## Expected Output

The CSV file will look like this:

| Article Title      | Author      | Views | Comments | Favorites | Heat Score | Article URL                  |
|--------------------|-------------|-------|----------|-----------|------------|------------------------------|
| Python Web Scraper | John Doe    | 1200  | 34       | 50        | 85         | https://example.com/article1 |
| Data Extraction    | Jane Smith  | 900   | 20       | 35        | 72         | https://example.com/article2 |

---

## Key Considerations

1. **Handle Pagination**: Use parameters like `page` and `pageSize` to navigate through multiple pages.
2. **API Rate Limits**: Avoid sending too many requests in a short time to prevent getting blocked.
3. **Error Handling**: Implement error handling for cases where the API response is missing fields.

---

## Final Notes

Using this approach, you can build a flexible and reusable Python crawler to extract rankings or other data from APIs. Save the data into structured formats like CSV to make analysis easy and efficient.

For automated scraping without worrying about CAPTCHAs or IP blocks, try ScraperAPI: 👉 [https://www.scraperapi.com/?fp_ref=coupons](https://www.scraperapi.com/?fp_ref=coupons)
