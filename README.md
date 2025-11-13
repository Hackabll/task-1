I have outlined a process for basic network discovery and security assessment using the Nmap tool.

This task involves actively scanning a local network to identify active devices, their open ports, and potential vulnerabilities based on the services running on those ports.

🛠️ Step-by-Step Guide to Completing the Task
1. Install Nmap from official website.
Action: Go to the official Nmap website (nmap.org) and download the appropriate installer for your operating system (Windows, macOS, or Linux).
Purpose: Nmap is the essential tool needed to perform the network scan.
2. Find your local IP range (e.g., 192.168.1.0/24).
Action: Open your command prompt/terminal and run the network configuration command for your OS:
Windows: ipconfig
Linux/macOS: ip a or ifconfig
Calculation: Look for your device's IP Address (e.g., 192.168.1.5). The IP Range for your local network is usually the first three octets followed by .0/24 (e.g., 192.168.1.0/24). The /24 tells Nmap to scan all 256 possible addresses in that range.
Purpose: This defines the target scope for your network scan.
3. Run: nmap -sS 192.168.1.0/24 to perform TCP SYN scan.
Action: Open your terminal and execute the command, replacing the example range with your actual local network range. You may need administrator/root privileges (sudo on Linux/macOS).
nmap -sS [Your_Local_IP_Range]
Explanation of Flag:
-sS: The TCP SYN scan (often called a "stealth scan"). It's fast and efficient because it doesn't complete the full TCP handshake, checking only for a SYN/ACK response to determine if a port is open.
Purpose: This is the core action to find active hosts and their open ports on the network.
4. Note down IP addresses and open ports found.
Action: As Nmap runs, it will print its results to the terminal. Manually record or scroll through the output, noting the IP addresses of discovered devices and the list of associated open ports (e.g., port 22, 80, 443, etc.).
Purpose: This data is the raw output you need for the subsequent analysis steps.
5. Optionally analyze packet capture with Wireshark.
Action: Before running the Nmap scan (Step 3), you can start a network traffic analyzer like Wireshark. Set Wireshark to capture traffic on the network interface you're using. After the scan, stop the capture and filter the results for traffic related to the Nmap scan (e.g., packets with the SYN flag).
Purpose: This step allows you to see exactly how the -sS scan works at the packet level and observe the TCP handshake process (or lack thereof).
6. Research common services running on those ports.
Action: For each open port number you noted (e.g., 21, 22, 23, 80, 3389), use Google or a port number reference resource to find the standard service associated with it.
Example: Port 80 is typically HTTP (web server), Port 22 is typically SSH (secure remote login).
Purpose: Understanding the service is crucial for identifying its function and any associated risks.
7. Identify potential security risks from open ports.
Action: Evaluate the services based on the environment:
Unnecessary Services: Are there ports open that shouldn't be? (e.g., Telnet on port 23, which is unencrypted, or SSH on an insecure device).
Default Services: Are the services using default or weak configurations?
Patching: Are these services/devices likely running outdated software with known vulnerabilities?
Purpose: This is the assessment part of the task—determining if the discovered open ports pose a threat.
8. Save scan results as a text or HTML file.
Action: To save the results directly when running the scan, use Nmap's output flags:
To save as a standard text file:
nmap -sS [Your_Local_IP_Range] -oN results.txt
To save as an HTML file (for easy viewing in a browser):
nmap -sS [Your_Local_IP_Range] -oX results.xml --stylesheet https://nmap.org/svn/docs/nmap.xsl > results.html
(The second command is more complex but produces a formatted HTML report.)
Purpose: Preserving the scan results for documentation, future reference, or reporting.
