# Exploit Automation Script for Umbraco CMS XSLT Injection

This repository contains a Bash script to exploit an XSLT injection vulnerability in Umbraco CMS. The script automates the process of authentication, payload delivery, and command execution, extracting and displaying the results.

## Features

- Logs in to the target Umbraco CMS instance using provided credentials.
- Delivers an XSLT payload for remote command execution.
- Extracts and displays the output of the executed command.
- Saves debugging information for failed attempts.

---

## Usage

### Syntax

```bash
./Umbrac-CMS-XSLT-RCE <username> <password> <target_url> <full_command>
```

### Example

```bash
./Umbrac-CMS-XSLT-RCE admin@htb.local password123 http://example.com "systeminfo"
```

---

## Prerequisites

The script requires the following tools:
- `curl`: For sending HTTP requests.
- `awk`: For processing text output.
- `sed`: For text substitution and HTML parsing.
- `grep`: For regex-based content extraction.
- `tr`: For character filtering and formatting.

If any of these tools are not available, the script will automatically attempt to install them.

### Automatic Installation of Dependencies

The script includes a function to check and install missing dependencies. You can run the script, and it will prompt you to install any missing tools.

---

## Installation

Clone this repository to your system:

```bash
git clone https://github.com/0xDTC/Umbraco-CMS-7.12.4-Authenticated-RCE.git
cd Umbraco-CMS-7.12.4-Authenticated-RCE
```

Make the script executable:

```bash
chmod +x Umbrac-CMS-XSLT-RCE
```

---

## Dependencies Check and Installation

The script includes an automatic dependency installation mechanism. If any required tools are not found on the system, the script will attempt to install them using `apt`.

```bash
# Dependency installation function
install_dependencies() {
    echo "[*] Checking and installing required dependencies..."
    for tool in curl awk sed grep tr; do
        if ! command -v $tool &> /dev/null; then
            echo "[!] $tool not found. Installing..."
            sudo apt update && sudo apt install -y $tool
        else
            echo "[+] $tool is already installed."
        fi
    done
}
```

This function will run before executing the main script logic.

---

## Debugging

If the exploit fails, the script saves the full server response to `debug_attack_response.html`. Review this file to identify potential issues with the payload or server response.

---

## Disclaimer

**This script is intended for educational purposes only.** Unauthorized use of this script against systems without explicit permission is illegal and unethical. The authors are not responsible for any misuse or damage caused by this script.

---


### Contributions

Feel free to contribute improvements or report issues via GitHub Pull Requests or Issues.
