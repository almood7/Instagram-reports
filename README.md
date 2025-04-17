from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.common.keys import Keys
from selenium.webdriver.chrome.options import Options
import time
import chromedriver_autoinstaller
USERNAME = 'your_username'
PASSWORD = 'your_password'
TARGET_ACCOUNT = 'target_username'
NUM_REPORTS = 5
def login(driver):
driver.get("https://www.instagram.com/accounts/login/")
time.sleep(4)
user_input = driver.find_element(By.NAME, "username")
pass_input = driver.find_element(By.NAME, "password")
user_input.send_keys(USERNAME)
pass_input.send_keys(PASSWORD)
pass_input.send_keys(Keys.RETURN)
time.sleep(5)
def report_account(driver):
driver.get(f"https://www.instagram.com/{TARGET_ACCOUNT}/")
time.sleep(5)
try:
menu = driver.find_element(By.XPATH, "//button[contains(@class, 'x1i10hfl')]")
menu.click()
time.sleep(2)
report = driver.find_element(By.XPATH, "//button[contains(text(), 'Report')]")
report.click()
time.sleep(2)
report_account = driver.find_element(By.XPATH, "//button[contains(text(), 'Report account')]")
report_account.click()
time.sleep(2)
reason = driver.find_element(By.XPATH, "//button[contains(text(), 'It\'s pretending to be someone else')]")
reason.click()
time.sleep(2)
me = driver.find_element(By.XPATH, "//button[contains(text(), 'Me')]")
me.click()
time.sleep(2)
except Exception as e:
print("Error during reporting:", e)
def main():
chromedriver_autoinstaller.install()
options =Options()
options.add_argument('--headless')
options.add_argument('--disable-gpu')
options.add_argument('--log-level=3')
driver =webdriver.Chrome(options=options)
try:
login(driver)
for i in range(NUM_REPORTS):
print(f"Sending report #{i+1}")
report_account(driver)
time.sleep(3)
finally:
driver.quit()
if __name__ == '__main__':
main()
# Install Selenium for browser automation
pip install selenium
