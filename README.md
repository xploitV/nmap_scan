# nmap_scan

This script automates the process of running an Nmap scan and generating a readable HTML report. The report is then opened in Firefox for easy viewing. This is useful for analyzing a system's open ports, services, and potential vulnerabilities.

---

```bash

#!/bin/bash

banner=""" 
*******************************************************
                    NMAP SCAN 
*******************************************************
Please wait while we generate the scan report in Firefox.
*******************************************************
"""
# Display banner
echo "$banner"

# Set the target and output file names
TARGET=$1
XML_OUTPUT="nmapresult.xml"
HTML_OUTPUT="nmapresult.html"

# Run the Nmap scan and save output to XML
echo "Running Nmap scan on $TARGET..."
nmap -sC -sV -oX "$XML_OUTPUT" "$TARGET"

# Convert the Nmap XML result to HTML
echo "Converting XML to HTML..."
xsltproc /usr/share/nmap/nmap.xsl "$XML_OUTPUT" -o "$HTML_OUTPUT"

echo "Conversion complete. HTML file saved as $HTML_OUTPUT"

# Open the HTML report in Firefox
firefox "$HTML_OUTPUT" &

