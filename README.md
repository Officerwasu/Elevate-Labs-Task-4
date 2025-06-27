# Cybersecurity Internship - Task 4: Firewall Setup and Use (Linux - UFW)

## Objective:
The objective of this task was to configure and test basic firewall rules on a Linux system using UFW (Uncomplicated Firewall) to allow or block network traffic. This involved understanding how firewalls filter traffic and gaining practical experience in managing firewall rules.

## Tools Used:
* Linux Terminal
* UFW (Uncomplicated Firewall)
* Telnet client (for testing)

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
```
**Blocking Inbound Traffic on Port 23 (Telnet):**
An inbound rule was added to block TCP traffic on port 23 (Telnet). UFW was then enabled.
```bash
$ sudo ufw deny 23/tcp
Skipping adding existing rule
Skipping adding existing rule (v6)
$ sudo ufw enable
Firewall is active and enabled on system startup
```
The `ufw status` command confirmed that inbound connections to port 23 (TCP) were denied for both IPv4 and IPv6.
```bash
$ sudo ufw status
Status: active

To          Action      From
--          ------      ----
23/tcp      DENY        Anywhere
23/tcp (v6) DENY        Anywhere (v6)
```

**Testing the Block Rule:**
A local Telnet connection attempt to 127.0.0.1 on port 23 was made to verify the rule. As expected, the connection was refused, indicating the firewall successfully blocked the traffic. 

```bash
$ telnet 127.0.0.1 23
Trying 127.0.0.1...
telnet: Unable to connect to remote host: Connection refused
```

**Allowing Inbound SSH (Port 22):**
A rule was added to allow inbound TCP traffic on port 22 for SSH.

```bash
$ sudo ufw allow 22/tcp
Rule added
Rule added (v6)
```
