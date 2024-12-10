# Cybersecurity Project: Port Scanner Implementation

## Objective
This project focuses on building a Python-based port scanner to detect open ports on a target system. It utilizes socket programming to establish connections with specific ports and identifies open ports, aiding in network security analysis and vulnerability assessment.

## Skills Learned
- Proficiency in Python programming and socket operations.
- Understanding of port scanning techniques and their applications in cybersecurity.
- Hands-on experience with real-time network interactions.
- Familiarity with using Python libraries such as `pyfiglet` for aesthetic outputs.
- Practical knowledge of TCP/IP protocols and port states.

## Tools Used
- **Python 3** for scripting.
- **pyfiglet** for generating ASCII art banners.
- **socket** library for network communication.
- **sys** for system-level operations.
- **datetime** for logging scan timestamps.

## Steps

### 1. Set Up the Environment
- Installed Python 3 and required libraries (`pyfiglet` and built-in modules `socket`, `sys`, and `datetime`).
- Verified network configurations for testing the scanner locally.

### 2. Implement ASCII Art Banner
- Integrated the `pyfiglet` library to create an ASCII art banner displaying the title "PORT SCANNER" for better visualization.

### 3. Define Target System
- Targeted localhost (`http://localhost:8000`) to test scanning functionality in a controlled environment.

### 4. Develop Port Scanning Logic
- Used the `socket` library to iterate through all ports (1 to 65535) and attempt a connection.
- Set a timeout of 0.5 seconds for each port connection attempt to balance speed and reliability.
- Implemented `connect_ex()` to check if a port is open (returns `0` if successful).

### 5. Error Handling
- Caught `KeyboardInterrupt` to allow graceful script termination by the user.
- Managed `socket.error` to handle unresponsive hosts or network issues.

### 6. Test and Analyze
- Conducted tests on localhost to identify open ports and verify the script’s accuracy.
- Logged open ports and scan timestamps for analysis.

## Results
- Successfully scanned all ports on the target system.
- Identified open ports and recorded them for further investigation.
- Demonstrated the utility of port scanning for network security audits.
![image](https://github.com/user-attachments/assets/80a7eb09-c5bb-4238-b119-87f1beb1e401)

## Example Code
```python
import pyfiglet
import sys
import socket
from datetime import datetime

# Display ASCII banner using pyfiglet
ascii_banner = pyfiglet.figlet_format("PORT SCANNER")
print(ascii_banner)

# Set the target to localhost (your laptop)
target = "http://localhost:8000"

# Display banner with scanning details
print("_" * 50)
print("Scanning Target: " + target)
print("Scanning started at: " + str(datetime.now()))
print("_" * 50)

try:
    # Scan ports from 1 to 65535
    for port in range(1, 65536):
        s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
        socket.setdefaulttimeout(0.5)

        # Try connecting to the port
        result = s.connect_ex((target, port))
        if result == 0:
            print(f"[*] Port {port} is open")
        s.close()

except KeyboardInterrupt:
    print("\nExiting :(")
    sys.exit()

except socket.error:
    print("Host not responding :(")
    sys.exit()
