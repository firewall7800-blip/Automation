from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.chrome.service import Service
from webdriver_manager.chrome import ChromeDriverManager
import time

def setup_driver():
    """Sets up the Chrome driver."""
    options = webdriver.ChromeOptions()
    # Optional: Run in headless mode (no GUI) for server environments
    # options.add_argument('--headless') 
    driver = webdriver.Chrome(service=Service(ChromeDriverManager().install()), options=options)
    return driver

def automate_demo_form():
    """Demonstrates basic form automation on a safe test site."""
    driver = setup_driver()
    
    try:
        print("Navigating to DemoQA...")
        driver.get("https://demoqa.com/text-box")
        
        # Wait for the page to load slightly
        time.sleep(2)
        
        print("Locating elements...")
        # Find the 'Full Name' input field
        name_input = driver.find_element(By.ID, "userName")
        
        # Find the 'Email Address' input field
        email_input = driver.find_element(By.ID, "userEmail")
        
        # Find the 'Current Address' textarea
        current_address_input = driver.find_element(By.ID, "currentAddress")
        
        # Find the 'Permanent Address' textarea
        permanent_address_input = driver.find_element(By.ID, "permanentAddress")
        
        print("Filling out the form...")
        # Send keys to the inputs
        name_input.send_keys("John Doe")
        email_input.send_keys("john.doe@example.com")
        current_address_input.send_keys("123 Main Street, Springfield")
        permanent_address_input.send_keys("Same as current address")
        
        # Find and click the Submit button
        submit_button = driver.find_element(By.ID, "submit")
        submit_button.click()
        
        print("Form submitted successfully!")
        
        # Verify output (optional)
        time.sleep(1)
        output_name = driver.find_element(By.ID, "name").text
        print(f"Verified Output Name: {output_name}")
        
    except Exception as e:
        print(f"An error occurred: {e}")
        
    finally:
        # Keep browser open for a few seconds so you can see the result
        time.sleep(5)
        driver.quit()
        print("Browser closed.")

if __name__ == "__main__":
    automate_demo_form()
