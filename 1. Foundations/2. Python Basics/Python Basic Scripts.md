\# 🐍 Python Security Scripts



========================================================



\## Overview



This document demonstrates three simple Python scripts commonly used for learning cybersecurity automation:



1\. Hostname Resolver

2\. Port Scanner

3\. Banner Grabber



These scripts introduce basic networking concepts used in many penetration testing tools.



\---



\# 🌐 Script 1: Hostname Resolver



\## Description



This script converts a hostname into its corresponding IP address using Python’s `socket` module.



This is commonly used during reconnaissance to identify where domains resolve.



\---



\## Python Script



```python

import socket



def resolve\_host(hostname: str) -> None:

&#x20;   try:

&#x20;       ip\_address = socket.gethostbyname(hostname)

&#x20;       print(f"\[+] Hostname: {hostname}")

&#x20;       print(f"\[+] IP Address: {ip\_address}")

&#x20;   except socket.gaierror:

&#x20;       print("\[-] Could not resolve hostname.")



if \_\_name\_\_ == "\_\_main\_\_":

&#x20;   target = input("Enter a hostname: ").strip()

&#x20;   resolve\_host(target)



========================================================



\## Example Usage:



python3 hostname\_resolver.py



\# Example:



Enter a hostname: google.com



Output:



\[+] Hostname: google.com

\[+] IP Address: 142.250.191.78

Security Relevance



Hostname resolution is useful during:



reconnaissance, target identification, domain enumeration, mapping attack surfaces



========================================================



\#🚪 Script 2: Python Port Scanner



\## Description



This script performs a basic TCP port scan against a target host.



It attempts to connect to specified ports and reports whether they are open or closed.



========================================================



import socket



def scan\_port(host: str, port: int) -> None:

&#x20;   try:

&#x20;       with socket.socket(socket.AF\_INET, socket.SOCK\_STREAM) as sock:

&#x20;           sock.settimeout(1)

&#x20;           result = sock.connect\_ex((host, port))

&#x20;           if result == 0:

&#x20;               print(f"\[+] Port {port} is open")

&#x20;           else:

&#x20;               print(f"\[-] Port {port} is closed")

&#x20;   except socket.error as error:

&#x20;       print(f"\[!] Socket error on port {port}: {error}")



def main() -> None:

&#x20;   target = input("Enter target IP or hostname: ").strip()

&#x20;   ports = input("Enter ports separated by commas (example: 22,80,443): ").strip()



&#x20;   try:

&#x20;       resolved\_target = socket.gethostbyname(target)

&#x20;       print(f"\[+] Scanning target: {target} ({resolved\_target})")

&#x20;   except socket.gaierror:

&#x20;       print("\[-] Could not resolve target.")

&#x20;       return



&#x20;   try:

&#x20;       port\_list = \[int(port.strip()) for port in ports.split(",")]

&#x20;   except ValueError:

&#x20;       print("\[-] Invalid port format.")

&#x20;       return



&#x20;   for port in port\_list:

&#x20;       scan\_port(resolved\_target, port)



if \_\_name\_\_ == "\_\_main\_\_":

&#x20;   main()



========================================================



\## Example Usage



python3 python-port-scanner.py



\# Example input:



scanme.nmap.org

22,80,443



Example output:



\[+] Scanning target: scanme.nmap.org (45.33.32.156)

\[+] Port 22 is open

\[+] Port 80 is open

\[-] Port 443 is closed



\# Security Relevance



Port scanning helps identify:



accessible services, possible vulnerabilities, attack surface on a target system



Tools like Nmap use similar networking logic at a much more advanced level.



========================================================



🏴 Script 3: Banner Grabber



\## Description



This script connects to a service and attempts to retrieve the service banner.



\# A banner may reveal:



software name, service version, operating system information



========================================================



import socket



def grab\_banner(host: str, port: int) -> None:

&#x20;   try:

&#x20;       with socket.socket(socket.AF\_INET, socket.SOCK\_STREAM) as sock:

&#x20;           sock.settimeout(2)

&#x20;           sock.connect((host, port))

&#x20;           banner = sock.recv(1024)

&#x20;           print(f"\[+] Banner from {host}:{port}")

&#x20;           print(banner.decode(errors="ignore"))

&#x20;   except socket.timeout:

&#x20;       print("\[-] Connection timed out.")

&#x20;   except ConnectionRefusedError:

&#x20;       print("\[-] Connection refused.")

&#x20;   except socket.gaierror:

&#x20;       print("\[-] Could not resolve host.")

&#x20;   except Exception as error:

&#x20;       print(f"\[!] Error: {error}")



def main() -> None:

&#x20;   host = input("Enter target IP or hostname: ").strip()

&#x20;   port\_input = input("Enter target port: ").strip()



&#x20;   try:

&#x20;       port = int(port\_input)

&#x20;   except ValueError:

&#x20;       print("\[-] Port must be a number.")

&#x20;       return



&#x20;   grab\_banner(host, port)



if \_\_name\_\_ == "\_\_main\_\_":

&#x20;   main()



========================================================



\## Example Usage



python3 python-banner-grabber.py



\# Example:



Enter target IP or hostname: scanme.nmap.org

Enter target port: 22



Output:



\[+] Banner from scanme.nmap.org:22

SSH-2.0-OpenSSH\_6.6.1p1 Ubuntu-2ubuntu2.13



\# Key Takeaways



These scripts demonstrate several important Python and networking concepts:



Python socket programming



host resolution



TCP connections



port scanning logic



banner grabbing techniques



user input handling



basic error handling



These are foundational skills for building more advanced cybersecurity tools.

