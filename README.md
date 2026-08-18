# Hatesh_Capstone
#Automated Pentest Tool

## Automated Security Assessment Framework

A Bash-based automated penetration testing and vulnerability assessment
tool for authorized security testing, cybersecurity labs, academic
projects, and security documentation.

The tool combines Nmap, Nikto, Nuclei, WHOIS, NSLookup, and other
assessment utilities with the Gemini API to automate vulnerability
analysis and generate a professional HTML Vulnerability Assessment
Report.

## Features

-   Information gathering using WHOIS and NSLookup
-   Nmap port scanning
-   Nmap service enumeration
-   Nmap vulnerability assessment
-   Nikto web vulnerability scanning
-   Nuclei vulnerability scanning
-   Full automated assessment
-   Automatic text report generation
-   Gemini AI vulnerability analysis
-   Professional HTML5 report generation
-   Critical, High, Medium, Low, and Informational severity statistics
-   Vulnerability Severity Distribution graph
-   Security score out of 100
-   Risk analysis
-   Prioritized remediation plan
-   Overall security posture
-   Final conclusion
-   Saved HTML report history
-   Automatic browser opening
-   Responsive and print-friendly report design
-   Offline-compatible HTML graph using embedded HTML/CSS/SVG

## Tools Used

  Tool       Purpose
  ---------- ---------------------------------------------------------------
  Nmap       Port scanning, service enumeration, and vulnerability scripts
  Nikto      Web server and web vulnerability assessment
  Nuclei     Template-based vulnerability scanning
  WHOIS      Domain/IP information gathering
  NSLookup   DNS lookup and enumeration
  Curl       Gemini API communication
  jq         JSON processing and API response parsing

## Requirements

The tool is designed for Kali Linux or another compatible Linux
environment.

Install the main dependencies:

``` bash
sudo apt update
sudo apt install nmap nikto curl jq whois dnsutils
```

Check Nuclei:

``` bash
nuclei -version
```

## Gemini API Configuration

The API key is not stored in the Bash script.

Set it in the current terminal session:

``` bash
export GEMINI_API_KEY="YOUR_API_KEY"
```

Never publish or commit the API key to a public repository.

## Gemini Model

The tool is configured to use:

``` text
gemini-3.6-flash
```

## Installation

Make the script executable:

``` bash
chmod +x automated_pentest.sh
```

Run the tool:

``` bash
./automated_pentest.sh
```

## Main Menu

``` text
[1]  Information Gathering
[2]  Network & Port Scanning
[3]  Service Enumeration
[4]  Vulnerability Assessment
[5]  Nikto Web Vulnerability Scan
[6]  Nuclei Vulnerability Scan
[7]  Full Automated Assessment
[8]  Generate Text Report
[9]  Generate AI HTML Vulnerability Report
[10] View HTML Reports
[11] Exit
```

## Assessment Workflow

### Information Gathering

Collects available information using WHOIS and NSLookup.

### Network and Port Scanning

Runs an Nmap TCP SYN scan:

``` bash
nmap -Pn -sS -T4 TARGET
```

### Service Enumeration

Runs Nmap service and default-script enumeration:

``` bash
nmap -Pn -sV -sC -T4 TARGET
```

### Vulnerability Assessment

Runs Nmap vulnerability scripts:

``` bash
nmap -Pn --script vuln -T4 TARGET
```

### Nikto

Performs a web server vulnerability assessment:

``` bash
nikto -h TARGET
```

Nikto requires a reachable HTTP/HTTPS service.

### Nuclei

Runs a Nuclei vulnerability scan:

``` bash
nuclei -u TARGET
```

### Full Automated Assessment

The full assessment combines:

1.  WHOIS
2.  Nmap port and service scan
3.  Nmap vulnerability scan
4.  Nikto
5.  Nuclei

## Report Locations

Text report:

``` text
~/pentest_reports/final_report.txt
```

HTML reports:

``` text
~/pentest_reports/html_reports/
```

Generated HTML files use timestamped names such as:

``` text
vulnerability_report_YYYYMMDD_HHMMSS.html
```

## Gemini AI HTML Report

After completing an assessment, select:

``` text
[9] Generate AI HTML Vulnerability Report
```

The collected scan evidence is sent to Gemini for analysis.

The AI report generator is instructed to:

-   Use only supplied scan evidence
-   Avoid fabricated vulnerabilities
-   Avoid invented CVEs and CVSS scores
-   Avoid invented ports and services
-   Mark unavailable information as `Not Available`
-   Mark insufficient evidence as `Requires Manual Verification`
-   Calculate statistics from actual findings
-   Generate a vulnerability severity graph
-   Generate a security score
-   Provide risk analysis
-   Provide remediation recommendations
-   Provide an overall security posture
-   Provide a final conclusion

## HTML Report Structure

The generated report contains:

1.  Professional Cover Page
2.  Executive Summary
3.  Assessment Overview
4.  Target Information
5.  Assessment Scope
6.  Assessment Methodology
7.  Tools Used
8.  Security Findings Summary
9.  Vulnerability Severity Distribution
10. Detailed Vulnerability Findings
11. Technical Assessment Results
12. Risk Analysis
13. Prioritized Remediation Plan
14. Overall Security Posture
15. Security Score
16. Final Conclusion
17. Legal / Authorization Notice

## Vulnerability Severity Graph

The report includes a graph titled:

``` text
Vulnerability Severity Distribution
```

It displays actual counts for:

-   Critical
-   High
-   Medium
-   Low
-   Informational

The graph uses embedded HTML/CSS/SVG and does not require Chart.js or
external JavaScript libraries.

Severity colors:

  Severity        Color
  --------------- ---------
  Critical        #DC2626
  High            #EA580C
  Medium          #D97706
  Low             #16A34A
  Informational   #2563EB

## Professional HTML Design

The generated report uses a cybersecurity/SOC-style design with:

-   Dark navy/blue theme
-   Professional cards
-   Severity badges
-   Summary statistics
-   Technical tables
-   Security score visualization
-   Vulnerability distribution graph
-   Risk analysis
-   Remediation tables
-   Responsive layout
-   Print-friendly CSS
-   Consistent left-aligned section headings
-   Professional footer

Major section headings are intentionally left aligned.

## Accuracy Rules

The AI report generator must not:

-   Fabricate findings
-   Invent CVEs
-   Invent CVSS scores
-   Invent services
-   Invent ports
-   Claim successful exploitation without evidence
-   Create fake statistics
-   Hide Critical or High findings

Unavailable information should be reported as:

``` text
Not Available
```

Insufficient evidence should be reported as:

``` text
Requires Manual Verification
```

## Network Lab Setup

For a Kali Linux and Metasploitable laboratory, both VMs must
communicate through the same Host-Only VMware network.

For example, if Metasploitable uses:

``` text
192.168.158.129
```

Kali must have a reachable interface on the corresponding network, such
as:

``` text
192.168.158.x/24
```

Verify connectivity before scanning:

``` bash
ping -c 3 192.168.158.129
```

If the host is unreachable, fix the VMware network configuration before
running Nikto, Nmap, or other scanners.

## Nikto Troubleshooting

Check whether HTTP or HTTPS is available:

``` bash
nmap -Pn -p 80,443 TARGET
```

For HTTP:

``` bash
nikto -h http://TARGET
```

For HTTPS:

``` bash
nikto -h https://TARGET
```

An error such as:

``` text
[FAIL] Unable to connect to TARGET:80
```

normally means the web service is not reachable on port 80. This is
generally a target, network, or web-service issue rather than a Nikto
installation issue.

## Example

Set the Gemini API key:

``` bash
export GEMINI_API_KEY="YOUR_API_KEY"
```

Start the tool:

``` bash
./automated_pentest.sh
```

Run a full assessment:

``` text
[7] Full Automated Assessment
```

Then generate the AI HTML report:

``` text
[9] Generate AI HTML Vulnerability Report
```

The report will be saved under:

``` text
~/pentest_reports/html_reports/
```

## Runtime Directory

``` text
~/pentest_reports/
├── final_report.txt
└── html_reports/
    ├── vulnerability_report_YYYYMMDD_HHMMSS.html
    └── ...
```

## Authorization Notice

This tool is intended only for authorized security assessments,
controlled cybersecurity laboratories, educational projects, and systems
for which explicit permission has been granted.

Do not use the tool against systems, networks, websites, or services
without authorization.

## Project Purpose

The project demonstrates how traditional security assessment utilities
can be combined with Bash automation and generative AI to streamline
vulnerability analysis and professional security reporting.

The automated workflow reduces manual report preparation by transforming
raw security assessment evidence into a structured HTML Vulnerability
Assessment Report.

## Project Information

**Student:** Hatesh Kumar\
**Course:** Cybersecurity\
**Instructor:** Sir Habibullah Nagraj\
**Project:** Automated Pentest Tool\
**Framework:** Automated Security Assessment Framework\
**AI Integration:** Gemini API
