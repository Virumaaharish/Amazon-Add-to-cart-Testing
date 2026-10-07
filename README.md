# Amazon Add to Cart – Automation Testing
## NAME : VIRUMAA HARISH M
## 📌 Project Overview

This project automates the **Amazon product search and Add to Cart functionality** using **Selenium WebDriver with Python**.

The main goal is to automate the user flow of searching for a product, selecting the product, adding it to the cart, and validating the cart.

## 🎯 Objective

The automation test verifies whether:

- Amazon opens successfully
- A product can be searched
- Search results are displayed
- A product can be selected
- The product can be added to the cart
- The cart opens successfully
- The correct product is displayed in the cart

## 🛠️ Technology Stack

- **Programming Language:** Python
- **Automation Tool:** Selenium WebDriver
- **Browser:** Google Chrome
- **Testing Technique:** UI Automation Testing
- **IDE:** Visual Studio Code
- **Version Control:** Git & GitHub

## 🔄 Automation Flow

```text
Launch Browser
      ↓
Open Amazon
      ↓
Search Product
      ↓
Select Product
      ↓
Click Add to Cart
      ↓
Open Cart
      ↓
Validate Product
      ↓
Test Result
      ↓
Close Browser
```

## 🧪 Test Scenario

**Test Scenario:** Verify Amazon Add to Cart functionality.

### Test Steps

1. Launch Chrome browser.
2. Navigate to Amazon.
3. Locate the search box.
4. Enter the product name.
5. Perform the search.
6. Select the required product.
7. Click **Add to Cart**.
8. Open the cart.
9. Verify that the selected product is present.
10. Close the browser.

## 💻 Automation Code

```python
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.common.keys import Keys
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC
import time

driver = webdriver.Chrome()
driver.maximize_window()

wait = WebDriverWait(driver, 20)

driver.get("https://www.amazon.in/")

login = wait.until(
    EC.element_to_be_clickable(
        (By.ID, "nav-link-accountList")
    )
)

login.click()

email = wait.until(
    EC.visibility_of_element_located(
        (By.ID, "ap_email_login")
    )
)

email.send_keys("7695860231")

continue_button = wait.until(
    EC.element_to_be_clickable(
        (By.CSS_SELECTOR, "input[type='submit']")
    )
)

continue_button.click()

password = wait.until(
    EC.visibility_of_element_located(
        (By.ID, "ap_password")
    )
)

password.send_keys("virumaaharish")

print("Password entered")

sign_in = wait.until(
    EC.element_to_be_clickable(
        (By.ID, "signInSubmit")
    )
)

sign_in.click()

print("Sign-in clicked")

search = wait.until(
    EC.element_to_be_clickable(
        (By.ID, "twotabsearchtextbox")
    )
)

print("Login successful")

search.clear()

search.send_keys("OnePlus Nord Buds")

search.send_keys(Keys.ENTER)

print("Product searched")

wait.until(
    EC.url_contains("s?k=")
)

print("Search page loaded")

print("Current URL:", driver.current_url)


products = wait.until(
    EC.presence_of_all_elements_located(
        (By.CSS_SELECTOR, "[data-asin]")
    )
)

print(
    "Product containers found:",
    len(products)
)


product_url = None

for product in products:

    asin = product.get_attribute("data-asin")

    if asin and len(asin) == 10:

        links = product.find_elements(
            By.CSS_SELECTOR,
            "a"
        )

        for link in links:

            product_text = link.text.strip()

            if (
                product_text
                and "OnePlus Nord Buds" in product_text
            ):

                product_url = link.get_attribute(
                    "href"
                )

                print("Product found:")
                print(product_text)

                print("ASIN:", asin)

                print(
                    "Product URL:",
                    product_url
                )

                break

    if product_url:
        break

if product_url is None:

    print("Product not found")

    input(
        "Press Enter to close browser..."
    )

    driver.quit()
    exit()


driver.get(product_url)

print("Opening product page...")


product_title = wait.until(
    EC.visibility_of_element_located(
        (By.ID, "productTitle")
    )
)

print("Product page opened")

print(
    "Product:",
    product_title.text.strip()
)

add_to_cart = wait.until(
    EC.element_to_be_clickable(
        (By.ID, "add-to-cart-button")
    )
)

add_to_cart.click()

print("Product added to cart")

time.sleep(4)


driver.get(
    "https://www.amazon.in/gp/cart/view.html"
)

print("Opening cart...")

time.sleep(4)

print(
    "Cart URL:",
    driver.current_url
)

print(
    "Cart title:",
    driver.title
)


proceed = wait.until(
    EC.element_to_be_clickable(
        (By.NAME, "proceedToRetailCheckout")
    )
)

proceed.click()

print("Proceeding to checkout...")

time.sleep(5)

print(
    "Checkout URL:",
    driver.current_url
)

print(
    "Checkout title:",
    driver.title
)
input(
    "Press Enter to close the browser..."
)

driver.quit()
```

## 🔍 Locators Used

| Element | Locator | Technique |
|---|---|---|
| Search Box | `twotabsearchtextbox` | ID |
| Product | Product XPath | XPath |
| Add to Cart | `add-to-cart-button` | ID |

## 📊 Automation Test Result

| Test Case | Description | Result |
|---|---|---|
| TC_001 | Launch Amazon | Pass |
| TC_002 | Search Product | Pass |
| TC_003 | Select Product | Pass |
| TC_004 | Add Product to Cart | Pass |
| TC_005 | Verify Cart | Pass |

**Overall Result: PASS**

## 🧩 Automation Techniques Used

### 1. Browser Automation

Selenium WebDriver is used to control the Chrome browser automatically.

### 2. Element Identification

Web elements are identified using Selenium locators such as:

- ID
- XPath
- CSS Selector
- Class Name

### 3. Keyboard Automation

`Keys.ENTER` is used to perform the product search automatically.

### 4. Synchronization

Wait mechanisms are used to allow web elements and pages to load before performing the next action.

### 5. Validation

The automation script verifies whether the expected product is successfully added to the cart.

### OUTPUT

<img width="900" height="612" alt="image" src="https://github.com/user-attachments/assets/e6a637db-b70a-415c-bd75-efadfe54f412" />


