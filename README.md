# Scraping-data-from-google-maps-using-python
A Python-based tool designed to efficiently extract business information and location data from Google Maps. This scraper automates data collection to provide structured datasets for market research and analysis. Ideal for projects requiring bulk geospatial data or local business insights. Efficient, scalable, and easy to customize.
Scraping data from Google Maps can provide valuable insights such as business names, ratings, addresses, and reviews. Below are two effective methods to achieve this using Python.

Method 1: Using Selenium for Web Automation

Steps:

Install Required Libraries Install Selenium and download the appropriate ChromeDriver for your browser version:

pip install selenium
Copy
Set Up Selenium Use Selenium to automate interactions with Google Maps:

from selenium import webdriver
from selenium.webdriver.common.by import By

# Configure ChromeDriver
options = webdriver.ChromeOptions()
options.add_argument('headless') # Run in background
driver = webdriver.Chrome(executable_path="path/to/chromedriver", options=options)

# Open Google Maps URL
url = "https://www.google.com/maps/place/Papa+John's+Pizza"
driver.get(url)

# Extract Data
title = driver.find_element(By.CLASS_NAME, "x3AX1-LfntMc-header-title-title").text
rating = driver.find_element(By.CLASS_NAME, "aMPvhf-fI6EEc-KVuj8d").text
print(f"Title: {title}, Rating: {rating}")

driver.quit()
Copy
Extract Additional Fields Modify the script to extract addresses, contact numbers, or reviews by targeting specific class names.

Method 2: Using BeautifulSoup with Selenium

Steps:

Install Dependencies Install BeautifulSoup and Selenium:

pip install beautifulsoup4 selenium
Copy
Scrape Data Use Selenium to load dynamic content and BeautifulSoup to parse HTML:

from bs4 import BeautifulSoup
from selenium import webdriver

driver = webdriver.Chrome(executable_path="path/to/chromedriver")
driver.get("https://www.google.com/maps/search/coffee")

soup = BeautifulSoup(driver.page_source, 'html.parser')

# Extract Business Names and Ratings
listings = soup.select('div.Nv2PK.THOPZb.CpccDe')
for listing in listings:
name = listing.select_one('div.qBF1Pd.fontHeadlineSmall').text.strip()
rating = listing.select_one('span.MW4etd[aria-hidden="true"]').text.strip() if listing.select_one('span.MW4etd[aria-hidden="true"]') else "No Rating"
print(f"Name: {name}, Rating: {rating}")

driver.quit()

<img width="367" height="211" alt="image" src="https://github.com/user-attachments/assets/ce69a091-77ae-41e3-b2bf-4617a2159c37" />
<img width="940" height="418" alt="image" src="https://github.com/user-attachments/assets/918102bf-0e9c-4d61-b5de-4b2b9dbc10a1" />
<img width="940" height="413" alt="image" src="https://github.com/user-attachments/assets/075b5e9b-aced-4a3b-81ea-9722443ebcb3" />
<img width="940" height="400" alt="image" src="https://github.com/user-attachments/assets/6478bcff-5e19-4422-b3ce-925d5dea4f97" />
<img width="940" height="442" alt="image" src="https://github.com/user-attachments/assets/bf6fa977-cbcc-4469-9fa7-37d3a6a9d3a5" />
<img width="827" height="443" alt="image" src="https://github.com/user-attachments/assets/53177877-a671-48cf-b118-8dc6ed041d56" />




