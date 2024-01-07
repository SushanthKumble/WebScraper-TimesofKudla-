
# Web Scraping with Python

This Python script utilizes the `requests`, `urllib.parse`, `BeautifulSoup`, and `fake_useragent` libraries to perform web scraping on a news website. The goal is to extract article headlines and summaries from the specified URL.

## Prerequisites

- Make sure you have Python installed on your system.
- Install the required libraries using the following command:

  ```
  pip install requests beautifulsoup4 fake_useragent
  ```

## Usage

1. Import necessary libraries at the beginning of your script:

   ```python
   import requests
   from urllib.parse import unquote
   from bs4 import BeautifulSoup
   from fake_useragent import UserAgent
   ```

2. Set up the base URL and initialize variables:

   ```python
   heading = []
   summary = []
   ```

3. Define the URL to scrape and set up the User-Agent for the request:

   ```python
   url = "https://www.timesofkudla.com/ARDC.in/category/ಟೈಮ್ಸ್-ಆಫ್-ಕುಡ್ಲ-ನ್ಯೂಸ್-times-of-kudla-n/page/{x}/"
   user_agent = UserAgent()
   headers = {'User-Agent': user_agent.random}
   ```

4. Make a request to the URL:

   ```python
   response = requests.get(url, headers=headers)
   ```

5. Print User-Agent and response status code for debugging:

   ```python
   print("User Agent:", headers['User-Agent'])
   print("Response Status Code:", response.status_code)
   ```

6. Parse the HTML content using BeautifulSoup:

   ```python
   response_content = response.content
   soup = BeautifulSoup(response_content, 'html.parser')
   ```

7. Loop through the HTML to extract headlines and summaries:

   ```python
   for x in range(0, 100):
       h2 = soup.find_all('h2', class_='card-title entry-title')
       for a_tag in h2:
           heading.append(a_tag.text)

       div = soup.find_all('div', class_="card-description entry-summary")
       for i in range(0, 10):
           first_div_element = div[i]
           p_tags = first_div_element.find_all('p')
           for p_tag in p_tags:
               p_tag_text = p_tag.get_text()
               summary.append(p_tag_text)
   ```

8. The `heading` list now contains the article headlines, and the `summary` list contains the corresponding summaries.

9. Customize the code as needed for your specific use case.

## Notes

- Ensure compliance with the website's terms of service and policies when scraping data.
- Adjust the code to handle pagination if the website spans multiple pages.

```

Feel free to modify and enhance the README based on your specific requirements and project details.
