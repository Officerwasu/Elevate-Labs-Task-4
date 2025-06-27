# Cybersecurity Internship - Task 4: Firewall Setup and Use (Linux - UFW)

## Objective:
The objective of this task was to configure and test basic firewall rules on a Linux system using UFW (Uncomplicated Firewall) to allow or block network traffic. This involved understanding how firewalls filter traffic and gaining practical experience in managing firewall rules.

## Tools Used:
* Linux Terminal
* UFW (Uncomplicated Firewall)
* Telnet client (for testing)

## Deliverables:
Screenshots demonstrating the configuration and testing of firewall rules are included below, represented by terminal output.

---

### Implementation Steps & Terminal Output:

**System Information:**
The task was performed on a Debian GNU/Linux 12 (bookworm) system. 

```bash
$ cat /etc/os-release
PRETTY_NAME="Debian GNU/Linux 12 (bookworm)"
NAME="Debian GNU/Linux"
VERSION_ID="12"
VERSION="12 (bookworm)"
VERSION_CODENAME=bookworm
ID=debian
HOME_URL="[https://www.debian.org/](https://www.debian.org/)"
SUPPORT_URL="[https://www.debian.org/support](https://www.debian.org/support)"
BUG_REPORT_URL="[https://bugs.debian.org/](https://bugs.debian.org/)"
