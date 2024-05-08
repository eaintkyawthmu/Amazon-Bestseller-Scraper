
# Amazon Bestseller Scraper


<a href="https://opensource.org/licenses/MIT/" target="_blank"><img alt="MIT License" src="https://img.shields.io/badge/License-MIT-blue.svg" style="display: inherit;"/></a>  <a href="https://github.com/eaintkyawthmu" target="_blank"><img alt="Eaint" src="https://img.shields.io/badge/Author-AngelicML-blue.svg" style="display: inherit;"/></a>

## About the Project

This is a step-by-step project tutorial on how to scrape the Amazon Bestsellers Fashion page using Python , Beautifulsoup and Selenium. This project is a part of my portfolio to showcase my skills in web scraping and data extraction.


You can reach out to me via :

[![Gmail Badge](https://img.shields.io/badge/-Email--me-c14438?style=flat-square&logo=Gmail&logoColor=white&link=mailto:eaintkyawthmu@gmail.com)](mailto:eaintkyawthmu@gmail.com) [![Medium Badge](https://img.shields.io/badge/-Medium-black?style=flat-square&logo=Medium&logoColor=white&link=https://medium.com/@eaintkyawthmu/)](https://medium.com/@eaintkyawthmu/)      [![Linkedin Badge](https://img.shields.io/badge/-Linkedin-blue?style=flat-square&logo=Linkedin&logoColor=white&link=https://www.linkedin.com/in/eaintkyawthmu/)](https://www.linkedin.com/in/eaintkyawthmu/)   [![GitHub Badge](https://img.shields.io/badge/-GitHub-black?style=flat-square&logo=github&logoColor=white&link=https://github.com/eaintkyawthmu/)](https://github.com/eaintkyawthmu) 
 


## Prerequisites

Before we begin, make sure you have the following prerequisites:

1. Python installed on your system.
2. pip (Python package manager) installed.
3. Chrome browser and driver installed.


#### URL to be scraped is - [https://www.amazon.com/gp/bestsellers/fashion/ref=zg-bs_fashion_dw_sml ](https://www.amazon.com/gp/bestsellers/fashion/ref=zg-bs_fashion_dw_sml)

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2023-11-04/ea26c518-5b08-4486-aa70-73d827919e89/user_cropped_screenshot.jpeg?tl_px=0,0&br_px=3160,1225&force_format=png&width=1120.0)

## Step 1: Install Selenium

To get started, we need to install the Selenium library. Open your terminal or command prompt and run the following command:

```bash
pip install selenium
```

## Step 2: Import Necessary Libraries

Create a Python script or Jupyter Notebook for your project and import the necessary libraries at the beginning of your script:

```python
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC
from bs4 import BeautifulSoup
```

These libraries will help us automate web scraping and parse HTML content.

## Step 3: Set Up Chrome Driver

We will use Selenium with a Chrome driver. Set up the Chrome driver in headless mode (i.e., without opening a visible browser window):

```python
options = webdriver.ChromeOptions()
options.add_argument('--headless')
driver = webdriver.Chrome(options=options)
```

This configuration allows us to run the scraping process silently.

## Step 4: Define the URL

Now, let's define the URL of the Amazon Bestsellers Fashion page we want to scrape:

```python
url = "https://www.amazon.com/gp/bestsellers/fashion/ref=zg-bs_fashion_dw_sml"
```

## Step 5: Navigate to the URL

Navigate to the URL using the Chrome driver and wait for the page to load:

```python
driver.get(url)
wait = WebDriverWait(driver, 10)
wait.until(EC.presence_of_element_located((By.CLASS_NAME, "p13n-desktop-grid")))
```

We are waiting for the element with the class name "p13n-desktop-grid" to ensure that the page has loaded before proceeding.

## Step 6: Find the Product Column

Next, we find the product column on the page using its class name:

```python
product_column = driver.find_element(By.CLASS_NAME, "p13n-desktop-grid")
```

## Step 7: Parse HTML Content

Parse the HTML content of the product column using BeautifulSoup:

```python
soup = BeautifulSoup(product_column.get_attribute('innerHTML'), 'html.parser')
```

## Step 8: Extract Product Details

Now, let's find all the product items on the page and extract their details:

```python
products = soup.find_all('div', class_='a-cardui _cDEzb_grid-cell_1uMOS expandableGrid p13n-grid-content')
for product in products:
    # Extract product name
    name = product.find('div', {'class': '_cDEzb_p13n-sc-css-line-clamp-3_g3dy1'}).text.strip()

    # Extract product review
    review = product.find('span', {'class':  'a-icon-alt'}).text.strip()

    # Extract product price
    price = product.find('span', {'class': '_cDEzb_p13n-sc-price_3mJ9Z'})
    if price is not None:
        price = price.text
    else:
        price = 'N/A'

    # Extract product link
    link = product.find('a', {'class': 'a-link-normal'})['href']

    print(f'Title: {name}')
    print(f'Review: {review}')
    print(f'Price: {price}')
    print(f'Product Link : https://www.amazon.com{link}')
    print("")
```

This code snippet extracts product names, reviews, prices, and links for each product and prints them to the console.

## Step 9: Run the Script

Save your Python script and run it. You should see the scraped product details 

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2023-11-05/567f1707-6b90-46a4-8676-db60f95bf579/user_cropped_screenshot.jpeg?tl_px=485,0&br_px=2205,960&force_format=png&width=1120.0)

That's it! Now you can scrape the Amazon Bestsellers Fashion page and extract product details using Python and Selenium. Remember to respect website scraping policies and terms of service when scraping any website.

---

Remember to be respectful of website scraping policies and terms of service when using this scraper.

Happy scraping!

## License
MIT © [Eaint Kyawt Hmu](https://www.linkedin.com/in/eaintkyawthmu/)

