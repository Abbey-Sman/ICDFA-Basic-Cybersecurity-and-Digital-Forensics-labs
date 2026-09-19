## Author

**Suleiman Abbey Bello**  
ICDFA Trainee, Cohort 11  
Fellowship in Cybersecurity and Digital Forensics

## License

# ICDFA Cybersecurity Labs: Reconnaissance and Web Security

![Program](https://img.shields.io/badge/Program-ICDFA-0D3265?style=for-the-badge)
![Labs](https://img.shields.io/badge/Labs-3-2ea44f?style=for-the-badge)
![Platform](https://img.shields.io/badge/Platform-Kali%20Linux-557C94?style=for-the-badge&logo=kalilinux&logoColor=white)
![Purpose](https://img.shields.io/badge/Purpose-Authorized%20Training-orange?style=for-the-badge)

A practical cybersecurity lab portfolio covering network and service reconnaissance, web application security testing, and Bash-based reconnaissance automation. The exercises are designed for controlled, instructor-authorized environments using intentionally vulnerable systems such as Metasploitable 2, DVWA, and Mutillidae.

> [!CAUTION]
> These labs are strictly for ethical, legal, and instructor-authorized security training. Do not scan, test, or automate reconnaissance against public systems, production infrastructure, or any target without explicit permission.

## Table of Contents

- [Overview](#overview)
- [Learning Objectives](#learning-objectives)
- [Lab Structure](#lab-structure)
- [Tools and Technologies](#tools-and-technologies)
- [Repository Structure](#repository-structure)
- [Lab 1: Network and Service Reconnaissance](#lab-1-network-and-service-reconnaissance)
- [Lab 2: Web Application Security Testing](#lab-2-web-application-security-testing)
- [Lab 3: Bash Reconnaissance Automation](#lab-3-bash-reconnaissance-automation)
- [Getting Started](#getting-started)
- [Evidence and Reporting](#evidence-and-reporting)
- [Security Recommendations](#security-recommendations)
- [Ethical Use](#ethical-use)
- [Author](#author)
- [License](#license)

## Overview

This repository documents three progressive laboratory assignments completed as part of the ICDFA cybersecurity and digital forensics training program:

1. **Network and service reconnaissance** using Nmap, Nmap Scripting Engine, curl, and WhatWeb.
2. **Web application security testing** using browser developer tools, Burp Suite, DVWA, Mutillidae, Nikto, DIRB, and controlled SQL injection verification.
3. **Bash reconnaissance automation** through an interactive tool-selection script for WhatWeb, Nmap, and DIRB.

The labs move from manual discovery and analysis to application-level testing and finally to safe task automation.

## Learning Objectives

By completing these labs, I developed practical experience in:

- Identifying hosts and validating connectivity in an isolated laboratory network.
- Discovering TCP and UDP ports, services, versions, and possible operating systems.
- Interpreting Nmap port states and service-enumeration output.
- Using safe NSE scripts to inspect HTTP, SMB, SSH, and FTP services.
- Fingerprinting web technologies with WhatWeb.
- Inspecting HTTP requests, responses, headers, cookies, and parameters.
- Intercepting and analyzing requests with Burp Suite.
- Evaluating file-upload validation using harmless test files.
- Performing web-server checks and content discovery with Nikto and DIRB.
- Observing SQL injection behavior in purposely vulnerable training applications.
- Using SQLMap within a restricted scope to verify approved lab metadata.
- Writing Bash scripts with variables, input handling, validation, functions, conditionals, and menus.
- Producing reproducible evidence and defensive recommendations.

## Lab Structure

| Lab | Focus | Main Tools | Target Environment |
|---|---|---|---|
| Lab 1 | Network and service reconnaissance | Nmap, NSE, curl, WhatWeb | Metasploitable 2 |
| Lab 2 | Web application security testing | Burp Suite, DVWA, Mutillidae, Nikto, DIRB, SQLMap | Intentionally vulnerable web apps |
| Lab 3 | Reconnaissance automation | Bash, Nmap, WhatWeb, DIRB | Instructor-authorized lab target |

## Tools and Technologies

- **Kali Linux**
- **Metasploitable 2**
- **Nmap and NSE**
- **WhatWeb**
- **curl**
- **Burp Suite**
- **DVWA**
- **OWASP Mutillidae II**
- **Nikto**
- **DIRB**
- **SQLMap**
- **Bash**

## Repository Structure

```text
.
├── Lab_1_Network_Service_Reconnaissance/
│   ├── README.md
│   ├── evidence/
│   └── results/
├── Lab_2_Web_Application_Security_Testing/
│   ├── README.md
│   ├── evidence/
│   └── results/
├── Lab_3_Bash_Reconnaissance_Automation/
│   ├── README.md
│   ├── recon_tool.sh
│   ├── evidence/
│   └── results/
├── .gitignore
└── README.md
```

> Store screenshots and sanitized outputs only. Never commit passwords, session cookies, authentication tokens, personal data, or sensitive infrastructure details.

## Lab 1: Network and Service Reconnaissance

### Objective

Build a clear inventory of an authorized Metasploitable 2 target by identifying reachable hosts, open ports, running services, software versions, operating-system indicators, and exposed web technologies.

### Core Activities

- Identified the Kali Linux and target IP addresses.
- Confirmed connectivity between virtual machines.
- Performed host discovery and default TCP scanning.
- Conducted version, operating-system, aggressive, full-port, and UDP scans.
- Used safe NSE scripts for HTTP, SMB, SSH, and FTP enumeration.
- Confirmed HTTP response information with `curl`.
- Compared WhatWeb fingerprinting at different aggression levels.
- Built a final service inventory from collected evidence.

### Representative Commands

```bash
# Confirm connectivity
ping -c 4 <target-ip>

# Host discovery
nmap -sn <network-range>

# Service and version detection
nmap -sV <target-ip>

# Full TCP service inventory
sudo nmap -p- -sV <target-ip>

# Common UDP service discovery
sudo nmap -sU --top-ports 20 -sV <target-ip>

# Safe default NSE enumeration
nmap -sC -sV <target-ip>

# HTTP title and headers
nmap -p 80 --script http-title,http-headers <target-ip>

# Web technology fingerprinting
whatweb -a 3 -v http://<target-ip>
```

### Key Deliverables

- Connectivity evidence.
- Host-discovery output.
- TCP and UDP scan results.
- Service and version inventory.
- OS-detection observations.
- NSE enumeration evidence.
- WhatWeb comparison.
- Final network/service table.

## Lab 2: Web Application Security Testing

### Objective

Assess how intentionally vulnerable applications handle HTTP traffic, uploads, directories, and database input while remaining within the instructor-approved scope.

### Core Activities

- Reviewed HTTP methods, headers, cookies, parameters, and status codes.
- Inspected baseline browser traffic with developer tools.
- Intercepted approved requests with Burp Suite.
- Tested DVWA file-upload behavior using harmless text files.
- Compared filename-extension and client-supplied MIME-type handling.
- Evaluated whether upload storage was web-accessible.
- Used Nikto to collect web-server configuration observations.
- Used DIRB to identify predictable or unlinked paths.
- Mapped user-controlled parameters in Mutillidae.
- Compared normal, true, and false input behavior in the approved SQL injection exercise.
- Used SQLMap only for authorized verification and metadata/schema enumeration.
- Documented defensive controls.

### Representative Commands

```bash
# Create a harmless upload file
echo 'ICDFA beginner upload test' > icdfa-upload-test.txt

# Web-server observations
nikto -h http://<target-ip> -output lab2-nikto.txt

# Content discovery
dirb http://<target-ip> -o lab2-dirb.txt

# Restricted SQLMap verification in the approved lab
sqlmap -u 'http://<target-ip>/<approved-path>?id=1' -p id --batch
```

### Defensive Takeaways

- Validate uploaded files server-side using allowlists and content inspection.
- Do not trust client-provided extensions or MIME types.
- Store uploads outside the web root or disable execution in upload directories.
- Generate safe server-side filenames and enforce size limits.
- Use parameterized queries or prepared statements for database operations.
- Return generic application errors while logging technical details securely.
- Apply least privilege to application database accounts.
- Protect cookies, tokens, and session information in reports and repositories.

## Lab 3: Bash Reconnaissance Automation

### Objective

Build an executable Bash script that prompts for an authorized target, validates user input, displays a menu, verifies tool availability, and runs the selected reconnaissance utility.

### Features

- No hardcoded target.
- Interactive IP address or domain input.
- Empty-input and whitespace validation.
- Menu-driven selection for WhatWeb, Nmap, or DIRB.
- Tool availability checks using `command -v`.
- Conditional routing with a Bash `case` statement.
- Clear handling of invalid selections.
- Direct execution using a shebang and executable permissions.

### Script

```bash
#!/usr/bin/env bash

echo "ICDFA Beginner Reconnaissance Tool"
echo "---------------------------------"
echo "Use only against authorised lab targets."
echo

read -rp "Enter authorised target IP address or domain: " target

if [[ -z "$target" ]]; then
    echo "Error: no target was entered."
    exit 1
fi

if [[ "$target" =~ [[:space:]] ]]; then
    echo "Error: target must not contain spaces."
    exit 1
fi

check_tool() {
    if ! command -v "$1" >/dev/null 2>&1; then
        echo "Error: required tool '$1' is not installed or not in PATH."
        exit 1
    fi
}

echo "Select a reconnaissance tool:"
echo "1) WhatWeb"
echo "2) Nmap"
echo "3) DIRB"
echo "4) Exit"
read -rp "Enter your choice [1-4]: " choice

case "$choice" in
    1)
        check_tool whatweb
        echo "[+] Running WhatWeb against $target"
        whatweb "http://$target"
        ;;
    2)
        check_tool nmap
        echo "[+] Running Nmap service detection against $target"
        nmap -sV "$target"
        ;;
    3)
        check_tool dirb
        echo "[+] Running DIRB against $target"
        dirb "http://$target"
        ;;
    4)
        echo "Exiting. No scan was run."
        exit 0
        ;;
    *)
        echo "Error: invalid menu choice."
        exit 1
        ;;
esac
```

### Run the Script

```bash
chmod +x recon_tool.sh
./recon_tool.sh
```

### Optional Output Management

```bash
mkdir -p results
nmap -sV "$target" | tee "results/nmap-$target.txt"
whatweb "http://$target" | tee "results/whatweb-$target.txt"
dirb "http://$target" | tee "results/dirb-$target.txt"
```

## Getting Started

### Prerequisites

- An isolated virtualization environment.
- Kali Linux or another authorized security-testing distribution.
- Metasploitable 2 and/or instructor-provided vulnerable web applications.
- Explicit authorization for every target.
- Required tools installed and available in `PATH`.

### Verify Tools

```bash
command -v bash
command -v nmap
command -v whatweb
command -v dirb
command -v nikto
command -v sqlmap
```

### Clone the Repository

```bash
git clone https://github.com/<your-username>/<repository-name>.git
cd <repository-name>
```

Replace placeholders such as `<target-ip>`, `<network-range>`, `<approved-path>`, `<your-username>`, and `<repository-name>` with values from your authorized lab environment.

## Evidence and Reporting

Recommended evidence for each activity includes:

- The command that was executed.
- A screenshot or sanitized text result.
- The date and lab environment.
- The objective of the test.
- A concise interpretation of the output.
- Any limitations or possible false positives.
- Defensive recommendations where applicable.

### Example Findings Format

```markdown
### Finding: Exposed Service

- **Target:** `<authorized-target>`
- **Port/Protocol:** `<port>/<protocol>`
- **Service:** `<service>`
- **Evidence:** `<sanitized command output or screenshot reference>`
- **Observation:** `<what the result indicates>`
- **Risk:** `<contextual risk in the lab environment>`
- **Recommendation:** `<defensive control>`
```

## Security Recommendations

1. Minimize externally accessible services and disable unnecessary ports.
2. Patch or replace outdated software and unsupported operating systems.
3. Segment vulnerable systems from production networks.
4. Use strong authentication and secure service configurations.
5. Validate all user-controlled input on the server.
6. Use prepared statements for database access.
7. Apply strict upload validation and non-executable storage.
8. Configure secure HTTP headers and generic error handling.
9. Log and monitor scanning, upload, authentication, and database events.
10. Retest controls in an authorized environment after remediation.

## Ethical Use

All commands and techniques in this repository are intended exclusively for:

- Instructor-authorized laboratory systems.
- Personally owned systems where explicit testing permission exists.
- Intentionally vulnerable applications created for education.

Do not use this material to access, disrupt, scan, or test systems without written authorization. The repository demonstrates defensive learning and responsible security practice, not unauthorized exploitation.

