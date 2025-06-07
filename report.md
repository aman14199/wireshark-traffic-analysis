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

Include screenshots in the `/screenshots/` folder showing:
- Nmap command output
- Hydra brute-force attempts
- Wireshark analysis with filters (e.g. `tcp.port == 22`, `tcp.flags.syn == 1`)

---

## 6. Recommendations

- Deploy fail2ban or SSH rate limiting.
- Monitor logs for repeated failed login attempts.
- Use an intrusion detection system (IDS) to detect port scans.

---

## 7. Conclusion

This project demonstrates detecting malicious traffic using Wireshark. Screenshots and filters highlight attacker behaviors and show how network-based attacks can be analyzed.

---

## 8. Author

Aman Sharma  
Cybersecurity & Network Analysis Enthusiast
