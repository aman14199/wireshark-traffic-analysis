# 📝 Detailed Analysis Report

## 1. Overview

This report analyzes SSH brute-force and port scanning attempts using Wireshark in a controlled lab environment.

---

## 2. SSH Brute-Force Analysis

- **Attack Tool**: Hydra with `rockyou.txt` wordlist.
- **Observed Behavior**:
  - The attacker’s IP repeatedly sends TCP SYN packets to the target on port 22.
  - Wireshark shows repeated SSH authentication attempts with failed logins.
  - Brute-force attempts are evident from consistent packet patterns and multiple failed login attempts.

- **Indicators**:
  - Repeated TCP SYN → SYN-ACK → RST.
  - Destination port consistently 22/tcp.
  - SSH protocol streams reveal key exchange attempts.

---

## 3. Port Scan Analysis

- **Attack Tool**: Nmap
- **Observed Behavior**:
  - The attacker’s IP sends a high volume of SYN packets to a range of destination ports.
  - Wireshark shows:
    - SYN-only packets for closed ports.
    - SYN-ACK responses from open ports.

- **Indicators**:
  - Sequential port numbers in the destination field.
  - SYN flags without corresponding ACK packets.

---

## 4. Indicators of Compromise (IoCs)

| Indicator             | Description           |
|-----------------------|-----------------------|
| Source IP: 192.168.x.x  | Attacker’s IP        |
| Destination IP: 192.168.x.x | Target’s IP      |
| Port: 22/tcp          | SSH brute-force       |
| Ports: 0-1000         | Nmap port scan range  |

---

## 5. Screenshots

Below are screenshots saved in the `/screenshots/` folder illustrating each analysis step:

| Screenshot | Description |
|------------|-------------|
| `screenshots/1.jpeg`  | Running Nmap on Kali Linux to scan the victim IP. |
| `screenshots/2.jpeg`  | Applying the filter `tcp.flags.syn == 1 && tcp.flags.ack == 0` in Wireshark to capture SYN packets. |
| `screenshots/3.jpeg`  | Applying the filter `ip.addr == 192.168.64.2` to isolate traffic. |
| `screenshots/4.jpeg`  | Simultaneously showing Kali command output and Wireshark capture. |
| `screenshots/5.jpeg`  | Displaying different color-coded outputs in Wireshark. |
| `screenshots/6.jpeg`  | Filtering using `ip.addr == 192.168.64.2`. |
| `screenshots/7.jpeg`  | Analyzing SYN packets with `tcp.flags.syn == 1 && tcp.flags.ack == 0`. |
| `screenshots/8.jpeg`  | Additional SYN packet analysis. |
| `screenshots/9.jpeg`  | Running Nmap scan on Kali and capturing packets on Ubuntu. |
| `screenshots/10.jpeg` | Running `sudo systemctl status ssh` on Ubuntu terminal. |
| `screenshots/11.jpeg` | Executing Hydra brute-force attack with specific commands on Kali. |
| `screenshots/12.jpeg` | Applying `tcp.port == 22` filter on Wireshark. |
| `screenshots/13.jpeg` | Visualizing different packet colors in Wireshark. |
| `screenshots/14.jpeg` | Following a TCP stream to analyze SSH attack traffic. |

---

## 6. Recommendations

- Deploy **fail2ban** or SSH rate limiting to prevent brute-force attempts.
- Monitor system logs for repeated failed SSH login attempts.
- Use strong, unique passwords and disable root login over SSH.
- Implement an Intrusion Detection System (IDS) to detect port scans and brute-force attempts.
- Keep systems updated with the latest security patches.

---

## 7. Conclusion

This project demonstrates how to detect malicious traffic using Wireshark. Screenshots and filters highlight attacker behaviors and show how network-based attacks can be analyzed effectively.

---

## 8. Author

**Aman Sharma**  
Cybersecurity & Network Analysis Enthusiast
