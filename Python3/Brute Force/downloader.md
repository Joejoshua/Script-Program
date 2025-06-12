# Simple File Downloader Script

This Python script demonstrates how to download a file from a given URL using the `requests` library. This can be useful for fetching wordlists, configuration files, or other resources during penetration testing or development.

Create a file named `downloader.py` and add the following content:
```python
#!/usr/bin/python3


# Imports the requests library to handle HTTP requests.
# Make sure you have 'requests' installed: pip install requests
import requests

# --- Configuration ---
# Set the URL of the file you want to download.
# IMPORTANT: Replace this with the actual URL you intend to use.
url = 'http://example.com/path/to/your/file.txt'

# Set the desired local filename for the downloaded content.
# This example saves it as 'downloaded_file.txt'.
output_filename = 'downloaded_file.txt'

try:
    print(f"[+] Attempting to download from: {url}")
    # Sends a GET request to the specified URL.
    # allow_redirects=True ensures that if the URL redirects, requests will follow it.
    r = requests.get(url, allow_redirects=True)

   # Check if the request was successful (status code 200)
    r.raise_for_status() # Raises an HTTPError for bad responses (4xx or 5xx)

    # Saves the downloaded file in binary mode ('wb').
    # Using binary mode is crucial for non-text files and generally safer.
    with open(output_filename, 'wb') as file:
        file.write(r.content)

    print(f"[+] File successfully downloaded and saved as '{output_filename}'")

except:
    print("Please check the URL and your internet connection.")
```

### How to Run
Execute the script from your terminal:
```bash
$ python3 downloader.py
```
Before running, make sure to modify the `url` and `output_filename` variables within the script to match your specific download target and desired local file name.

---