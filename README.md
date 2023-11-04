# Amazon Bestseller Scraper


we will explore how to scrape the Amazon Bestsellers Fashion page using Python and Selenium.

To begin, we need to install the Selenium library by running the following command:

```python
%pip install selenium

```

Next, we import the necessary libraries:

```python
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC
from bs4 import BeautifulSoup

```

We also set up the Chrome driver in headless mode:

```python
options = webdriver.ChromeOptions()
options.add_argument('--headless')
driver = webdriver.Chrome(options=options)

```

Now, let's define the URL of the page we want to scrape:

```python
url = "<https://www.amazon.com/gp/bestsellers/fashion/ref=zg-bs_fashion_dw_sml>"

```

We navigate to the URL and wait for the page to load:

```python
driver.get(url)
wait = WebDriverWait(driver, 10)
wait.until(EC.presence_of_element_located((By.CLASS_NAME, "p13n-desktop-grid")))

```

We find the product column using its class name:

```python
product_column = driver.find_element(By.CLASS_NAME, "p13n-desktop-grid")

```

Next, we parse the HTML content using BeautifulSoup:

```python
soup = BeautifulSoup(product_column.get_attribute('innerHTML'), 'html.parser')

```

Now, let's find all the product items and extract their details:

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
    print(f'Product Link : <https://www.amazon.com>{link}')
    print("")

```

And that's it! By following this guide, you can scrape the Amazon Bestsellers Fashion page and extract product details using Python and Selenium.

Remember to respect website scraping policies and terms of service when scraping any website.

Happy scraping!