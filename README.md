---
# LinkedIn Profile Scraper using Selenium and BeautifulSoup

This Python project scrapes LinkedIn profile data such as names, headlines, locations, emails, and phone numbers using Selenium for web automation and BeautifulSoup for HTML parsing. The scraped data is saved into an Excel file for further analysis.

## Features

- **Login to LinkedIn**: Automates the process of logging in to LinkedIn using your credentials.
- **Profile Scraping**: Extracts key details from a list of LinkedIn profiles (name, headline, location, email, and phone numbers).
- **Data Storage**: Saves the scraped information into an Excel file for later use.
- **Error Handling**: Handles errors during the scraping process to ensure the code runs smoothly even if some elements are missing from profiles.

## Setup and Installation

1. **Install Dependencies**:
   This project uses the following Python libraries:
   - `selenium`
   - `beautifulsoup4`
   - `openpyxl`
   - `pandas`
   
   You can install them using pip:
   ```bash
   pip install selenium beautifulsoup4 openpyxl pandas
   ```

2. **Selenium WebDriver**:
   - Download the appropriate Chrome WebDriver from [here](https://sites.google.com/a/chromium.org/chromedriver/downloads) and make sure it matches your Chrome browser version.
   - Extract it and place it in a directory accessible by the script.

## Usage

1. **Login to LinkedIn**:
   The script starts by automating the login process to LinkedIn. Replace `'Enter your Username'` and `'Enter passward here'` with your LinkedIn login credentials in the code:
   ```python
   username.send_keys('Enter your Username')  # Replace with your email
   password.send_keys('Enter passward here')  # Replace with your password
   ```

2. **List of LinkedIn Profiles**:
   Update the list `lis` with the LinkedIn profile URLs you wish to scrape:
   ```python
   lis = ["Enter the list of linkedIn links here"]
   ```

3. **Scraping Process**:
   The script navigates to each profile and extracts:
   - **Name**: The user's full name.
   - **Headline**: The user's professional headline.
   - **Location**: The user's location.
   - **Emails**: Any emails found using regular expressions.
   - **Phone Numbers**: Any phone numbers found using regular expressions.
   
   Each profile’s data is appended to a list and later saved into an Excel file.

4. **Running the Script**:
   Run the script using a Python interpreter. Make sure your Selenium WebDriver is correctly installed and your LinkedIn credentials are valid. The output will be stored in an Excel file:
   ```bash
   python linkedin_scraper.py
   ```

5. **Output**:
   The scraped data is saved into an Excel file named `LinkedIn_Scraped_Data_With_Education_23.xlsx`.

## Code Explanation

- **Selenium WebDriver Setup**:
   ```python
   driver = webdriver.Chrome()  
   driver.get('https://www.linkedin.com/login')
   ```
   This part initializes the Selenium WebDriver for Chrome and opens the LinkedIn login page.

- **Login Automation**:
   ```python
   username.send_keys('Enter your Username')
   password.send_keys('Enter passward here')
   driver.find_element(By.XPATH, '//button[@type="submit"]').click()
   ```
   The username and password are entered into the LinkedIn login form, and the login button is clicked.

- **Scraping Loop**:
   The code loops over the list of LinkedIn URLs, navigating to each profile and extracting the data using XPath selectors. Here are a few key points:
   - **Extracting Name**:
     ```python
     name_element = driver.find_element(By.XPATH, "//h1[@class = 'text-heading-xlarge inline t-24 v-align-middle break-words']")
     name = name_element.text.strip()
     ```
     The XPath is used to find the element containing the profile’s name.
   
   - **Extracting Emails**:
     Emails are extracted from the ‘About’ section using regular expressions:
     ```python
     email_pattern = r'[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}'
     emails = re.findall(email_pattern, about_text)
     ```

- **Saving the Data**:
   The extracted data is stored in a Pandas DataFrame and then exported to an Excel file:
   ```python
   df = pd.DataFrame(data)
   df.to_excel('LinkedIn_Scraped_Data_With_Education_23.xlsx', index=False)
   ```

## Notes

- **Delay for Page Load**:
   Time delays (`time.sleep(5)`) are added to ensure that the pages fully load before extracting elements.
- **Error Handling**:
   If any element (e.g., name, location) is not found on a profile, default values like `"Name not found"` are used, and the program continues without crashing.

## License

This project is licensed under the MIT License.

---

You can modify the placeholder values (like the LinkedIn URLs, username, and password) before using it. Let me know if you need any further adjustments!
