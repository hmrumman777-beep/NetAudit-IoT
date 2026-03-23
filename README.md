# UPnP-Exploit-Auditor 
**Advanced Research Tool for libupnp Vulnerabilities**

This repository contains professional research and a reconnaissance tool focused on **libupnp 1.6.19** memory corruption vulnerabilities (specifically **CVE-2012-5958**).

## Key Features
- **Version Fingerprinting:** Detects vulnerable libupnp SDK versions.
- **XML Fuzzing:** Automatically discovers hidden UPnP device description files.
- **SOAP Header Analysis:** Analyzes responses for potential injection points.

## Usage
```bash
pip install -r requirements.txt  
python3 UPnP-Exploiter.py <Router-IP>