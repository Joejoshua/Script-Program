# Password Generator Script
This Python script generates lists of simple passwords, primarily intended for **testing and educational purposes only**. It can create numerical or alphanumeric sequences, useful for populating wordlists for security assessments.

Create a file named `password-generator.py` and add the following content:

```python
#!/usr/bin/python3

import string

# --- Configuration Options ---
# Uncomment one of the options below to choose your password generation method.

# Option 1: Generate passwords like 000A to 999Z (3 digits + 1 uppercase letter)
# password_list = [f"{str(i).zfill(3)}{letter}" for i in range(1000) for letter in string.ascii_uppercase]

# Option 2: Generate passwords like 0000 to 9999 (4-digit numerical passwords)
password_list = [str(i).zfill(4) for i in range(10000)]
# -----------------------------

# Define the output file name
output_filename = "passwords.txt"

# Write each generated password on a new line to the specified file
with open(output_filename, "w") as file:
    for password in password_list:
        file.write(f"{password}\n")

print(f"Generated {len(password_list)} passwords and saved them to '{output_filename}'")
```

### How to Run
Execute the script from your terminal.
```bash
$ python3 scripts/password-generator.py
```

Alternatively, you can make the script executable and run it directly:
```bash
$ chmod +x scripts/password-generator.py
$ ./password-generator.py
```
This will create a file named `passwords.txt` in the same directory where you run the script, containing the generated passwords, each on a new line.

---