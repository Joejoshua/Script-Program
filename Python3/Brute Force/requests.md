# Basic HTTP Request Script
This Python script illustrates how to perform fundamental HTTP GET and POST requests using the powerful `requests` library. It's a foundational script for interacting with web applications, whether for testing, automation, or data retrieval.

Create a file named `requests_example.py` and add the following content:
```python
#!/usr/bin/python3

import requests
import re # Used for regular expression operations

# --- Configuration ---
# The target URL for the HTTP requests.
target_url = "https://example.com/login" # Example: a login page

# Data to be sent with a POST request (e.g., username and password for a form).
# Modify these values to match your specific target's form fields.
post_data = {'username':'testuser', 'password':'testpassword'}
# ---------------------

# It's good practice to verify the python3 executable path.
# On your terminal: $ which python3
# This command finds the exact location of the `python3` executable that the system will run.

# Create a session object to persist parameters across requests (e.g., cookies).
session = requests.Session()

try:
    print(f"[+] Performing HTTP requests to: {target_url}")

    # --- Example GET Request ---
    # Uncomment the lines below to perform a GET request.
    # print("\n--- Performing GET Request ---")
    # get_response = session.get(target_url, timeout=10)
    # print(f"GET Status Code: {get_response.status_code}")
    # print("GET Response Content (first 500 chars):\n", get_response.text[:500])

    # --- Example POST Request ---
    print("\n--- Performing POST Request ---")
    # Sends a POST request with the specified data.
    post_response = session.post(target_url, data=post_data, timeout=10) # Added timeout
    content = post_response.text

    print(f"POST Status Code: {post_response.status_code}")
    print("POST Response Content (first 500 chars):\n", content[:500])

    # --- Example of using regular expressions to find specific keywords ---
    # Uncomment the line below and modify the regex to search for specific patterns.
    # print("\n--- Searching for Keywords ---")
    # found_keywords = re.findall(r'Login successful|Welcome back', content, re.IGNORECASE)
    # if found_keywords:
    #    print(f"Found indicators: {found_keywords}")
    # else:
    #    print("No specific success indicators found in response.")

except:
    print("Please check the URL and your internet connection.")
```

### How to Run
Execute the script from your terminal:
```bash
$ python3 requests.py
```
Alternatively, you can make the script executable and run it directly:
```bash
$ chmod +x requests_example.py
$ ./requests.py
```
**Remember to update `target_url` and `post_data` in the script** to match the web application you are interacting with.

---