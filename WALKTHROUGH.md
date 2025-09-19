# Project Context

In cybersecurity, one common defense strategy is to only allow access from trusted IP addresses. These are stored in a file called allow_list.txt.

Over time, some IPs need to be removed — for example, when a device is no longer authorized. Doing this manually is slow and error-prone, so I built a Python script that automates the process.

 ## Objective

- Read the file of approved IPs (allow_list.txt)
- Compare it against a removal list (remove_list)
- Delete any unauthorized IPs automatically
- Save the updated list back into the file
- Package everything into a reusable function for future updates

---

## Step-by-Step Walkthrough

### Step 1: Define the Files and Lists
```py
import_file = "allow_list.txt"  
remove_list = ["192.168.97.225", "192.168.158.170", "192.168.201.40", "192.168.58.57"]
```
![define file](Assign_file.png)

> This step sets up the inputs: the file we’re working on, and the IPs to be removed.

---

### Step 2: Read the File Contents
```py
with open(import_file, "r") as file:
    ip_addresses = file.read()

print(ip_addresses)  # shows all IPs in one block of text

```

![Read file](open_textfile.png)


> Loaded all IP addresses into memory so Python can work with them.

---

### Step 3: Convert to a List
```py
ip_addresses = ip_addresses.split()
print(ip_addresses)  # now each IP is separated into a list

```
![convert to list](change_to_list.png)

> Split the text into a list format, making it easier to check and remove entries.

---

### Step 4: Remove Unauthorized IPs
```py
for element in ip_addresses:
    if element in remove_list:
        ip_addresses.remove(element)ist

print(ip_addresses)  # only valid IPs remain

```

> Compared each IP with the removal list. If a match was found, it was removed.

![Remove unauthorized IPs](remove_IPs.png)

---

### Step 5: Rewrite the File
```py
ip_addresses = " ".join(ip_addresses)

with open(import_file, "w") as file:
    file.write(ip_addresses)
```

![Rewrite textfile](Rewrite_file_to_string.png)

> Saved the updated list back into the file, replacing the old version.

---

### Step 6: Wrap It Into a Function
```py
def update_file(import_file, remove_list):
    with open(import_file, "r") as file:
        ip_addresses = file.read().split()

    for element in ip_addresses:
        if element in remove_list:
            ip_addresses.remove(element)

    ip_addresses = " ".join(ip_addresses)

    with open(import_file, "w") as file:
        file.write(ip_addresses)
```


> Created a reusable function so anyone can update the allowlist with one line of code.

---

🔹 Step 7: Test the Function
update_file("allow_list.txt", ["192.168.25.60", "192.168.140.81", "192.168.203.198"])

![Test function with another list](test-function.png)

> Successfully tested with another set of IPs — the function worked as expected.

---

### Example Outputs

**Before Cleanup:**

> ip_address 192.168.205.12 192.168.97.225 192.168.201.40


**After Cleanup:**

> ip_address 192.168.205.12

---

### Key Lessons
- **Automation:** Reduced manual errors and saved time
- **Python for Cybersecurity:** Applied scripting to real security tasks
- **Access Control:** Strengthened defenses by ensuring only valid IPs remain
- **Reusable Code:** Created a function that works for any new list of IPs
