# Selenium Web Scraping Automation: Price Tracking and Data Logging

**Selenium Web Scraping Automation** is a Python-based tool that automatically tracks product prices from e-commerce websites and logs the data into a CSV file. It eliminates the need for constantly refreshing pages to catch price changes, helping you stay on top of deals effortlessly.

## Tech Stack
- **Python**: The versatile language that runs the show.
- **Selenium**: The trusty sidekick that does all the heavy lifting for web scraping and automation.
- **CSV**: To neatly store all the price tracking data.
- **Fake User-Agent**: To make sure your requests aren’t blocked by websites.
- **ChromeDriver**: To run everything smoothly on the Chrome browser.

## Key Features:
- **Track product prices**: Monitor prices from your chosen online store.
- **Automatic logging**: It tracks prices and saves them in a CSV file without you lifting a finger.
- **Price threshold alerts**: Set your desired price and get notified when the product drops (email notifications using SMTP!).
- **Runs in the background**: It works silently while you go on with your day.

## How to Install:
1. **Clone the repository**:
    ```bash
    git clone https://github.com/AvianshManyam/SeleniumScraper
    ```
2. **Navigate to the project folder**:
    ```bash
    cd SeleniumScraper
    ```
3. **Install the required libraries**:
    ```bash
    pip install -r requirements.txt
    ```

## How to Use:
1. **Set the product URL**: Find the product you want to track (from sites like Myntra, Amazon, etc.), and paste the URL into the script.
   
2. **Find the HTML elements for product name and price**:
   - Open the product page in your browser.
   - Right-click on the product name and price, then select **Inspect** (or press `Ctrl+Shift+I`).
   - Copy the **XPath** or **CSS selector** for the product name and price.
   - Update the script with these values so the tool knows what to look for on the page.

3. **Set your price threshold**: If you're waiting for a price drop, set your price threshold in the script. Once the price hits your set amount, the script will log it for you.

4. **Run the script**:
    ```bash
    python price_tracking.ipynb
    ```
5. The script will start tracking the price and will save all the details in a CSV file (because who doesn't love organized data?).

(You can also add email notifications using the SMTP library! Just update the script to send an email when the price drops below your threshold.)

## How to Add Email Notifications (Optional):
If you’d like to receive an email when the price drops, you can add the following SMTP code to the script:

### Example SMTP Code:

```python
import smtplib
from email.mime.text import MIMEText
from email.mime.multipart import MIMEMultipart

def send_email(price, product_name):
    # Set up your email credentials and SMTP server
    sender_email = "your_email@gmail.com"
    receiver_email = "recipient_email@gmail.com"
    password = "your_email_password"

    subject = f"Price Drop Alert: {product_name}"
    body = f"The price of {product_name} has dropped to {price}. Grab it now!"

    # Create the email
    msg = MIMEMultipart()
    msg['From'] = sender_email
    msg['To'] = receiver_email
    msg['Subject'] = subject
    msg.attach(MIMEText(body, 'plain'))

    # Set up the SMTP server and send the email
    try:
        server = smtplib.SMTP('smtp.gmail.com', 587)
        server.starttls()
        server.login(sender_email, password)
        text = msg.as_string()
        server.sendmail(sender_email, receiver_email, text)
        server.quit()
        print("Email sent successfully!")
    except Exception as e:
        print(f"Error sending email: {e}")
