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
The `ufw status` command now showed both the denial rule for port 23 and the allow rule for port 22.

```bash
$ sudo ufw status
Status: active

To          Action      From
--          ------      ----
23/tcp      DENY        Anywhere
22/tcp      ALLOW       Anywhere
23/tcp (v6) DENY        Anywhere (v6)
22/tcp (v6) ALLOW       Anywhere (v6)
```

**Removing the Test Block Rule:**
To revert the firewall to its original state or for further configuration, the previously added block rule for port 23 was removed. First, the rules were listed with numbers.

Then, the rule at index 1 (blocking 23/tcp for IPv4) and index 3 (blocking 23/tcp for IPv6) were deleted.
```bash
$ sudo ufw status numbered
Status: active

To          Action      From
--          ------      ----
[1] 23/tcp    DENY IN     Anywhere
[2] 22/tcp    ALLOW IN    Anywhere
[3] 23/tcp (v6) DENY IN     Anywhere (v6)
[4] 22/tcp (v6) ALLOW IN    Anywhere (v6)

$ sudo ufw delete 1
Deleting:
 deny 23/tcp
Proceed with operation (y/n)? y
Rule deleted

$ sudo ufw delete 3
Deleting:
 deny 23/tcp
Proceed with operation (y/n)? y
Rule deleted
```
### Summary of How a Firewall Filters Traffic:
A firewall acts as a security guard for a network, controlling the flow of traffic based on a predefined set of rules. It sits at the perimeter of a network (or on a host) and inspects incoming and outgoing data packets.

#### Here's how it generally filters traffic:

*  **Rule-Based Filtering:** Firewalls operate on rules that specify what traffic is allowed or denied. These rules can be based on various criteria, including source and destination IP addresses, port numbers (e.g., port 23 for Telnet, port 22 for SSH), protocols (TCP, UDP, ICMP), and even the state of a connection.
*  **Packet Inspection:** When a data packet arrives at the firewall, it is inspected against the configured rules. If a packet matches a rule that denies access, it is dropped (blocked). If it matches a rule that allows access, it is permitted to pass through.
*  **Inbound vs. Outbound Rules:**
    * Inbound rules govern traffic attempting to enter the protected network or host.  For example, blocking port 23 inbound prevents external connections to the Telnet service on the system.
    * Outbound rules govern traffic originating from inside the protected network or host and attempting to leave. 

*  **Stateful vs. Stateless:**

    * Stateless firewalls inspect each packet individually without considering its relationship to other packets. This can be less secure as they don't track the context of a conversation.
    * Stateful firewalls (like UFW, which leverages iptables capabilities) are more common and keep track of the "state" of active connections. This means they can allow return traffic for an established outbound connection without an explicit inbound rule for that specific return traffic, significantly improving security and efficiency. 

By implementing these filtering mechanisms, firewalls prevent unauthorized access, block malicious traffic, and help protect systems from various cyber threats, significantly enhancing network security.
