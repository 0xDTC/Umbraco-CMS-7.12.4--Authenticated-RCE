# XSLT Injection Exploit Script

This Bash script demonstrates an XSLT injection attack targeting a vulnerable endpoint in an Umbraco CMS instance. It uses crafted payloads to execute arbitrary commands on the target system.

---

## **Features**
- **Authentication:** Logs in to the target system using supplied credentials.
- **Token Extraction:** Fetches and utilizes necessary CSRF and view state tokens dynamically.
- **Payload Delivery:** Injects a malicious XSLT payload for command execution.
- **Debugging Support:** Saves HTTP responses to debug files for troubleshooting.

---

## **Requirements**
- **System Requirements:**
  - `curl`: For making HTTP requests.
  - `grep`: For parsing responses.
  - `tr`: For handling cookies.
- **Target:** A vulnerable instance of Umbraco CMS.
- **Credentials:** Valid username and password for the target system.

---

## **Usage**

### **1. Script Syntax**
```sh
./exploit.sh <username> <password> <target_url> <full_command>
```

### **2. Parameters**
- `<username>`: The username for authentication.
- `<password>`: The password for authentication.
- `<target_url>`: The base URL of the target system.
- `<full_command>`: The command to execute on the target system.

### **3. Example**
```sh
./exploit.sh admin@htb.local baconandcheese http://remote.htb/ "whoami"
```

---

## **How It Works**

1. **Authentication:**
   - Sends a login request to the `/umbraco/backoffice/UmbracoApi/Authentication/PostLogin` endpoint.
   - Extracts cookies and CSRF tokens from the response.

2. **Fetching Tokens:**
   - Accesses the `/umbraco/developer/Xslt/xsltVisualize.aspx` page to retrieve `VIEWSTATE` and `VIEWSTATEGENERATOR` tokens.

3. **Payload Delivery:**
   - Constructs an XSLT payload with the command specified by the user.
   - Sends the payload to the target using the tokens and cookies from previous steps.

4. **Debugging:**
   - Saves responses to:
     - `debug_login_response.txt`: For debugging login issues.
     - `debug_xslt_response.html`: For debugging token retrieval issues.
     - `debug_attack_response.html`: For debugging payload delivery issues.

---

## **File Descriptions**
- `exploit.sh`: The main script.
- `debug_login_response.txt`: Stores the login HTTP response headers for debugging.
- `debug_xslt_response.html`: Stores the response from the XSLT visualization page for debugging.
- `debug_attack_response.html`: Stores the response after payload delivery for debugging.

---

## **Sample Output**
```sh
[*] Step 1 - Logging in...
[+] Login successful!

[*] Step 2 - Accessing XSLT Visualize page...
[+] Successfully fetched tokens.

[*] Step 3 - Sending malicious payload...
[+] Payload executed successfully. Check the target!

[*] Exploit completed.
```

---

## **Troubleshooting**
1. **Login Issues:**
   - Check `debug_login_response.txt` for response headers.
   - Verify the provided username and password.

2. **Token Retrieval Issues:**
   - Check `debug_xslt_response.html` for valid `VIEWSTATE` and `VIEWSTATEGENERATOR` tokens.

3. **Payload Delivery Issues:**
   - Review `debug_attack_response.html` for error details.
---

## **Disclaimer**
This script is for **educational purposes only**. Unauthorized use against systems without explicit permission is illegal. Use this script responsibly.