
# Task 4 — Firewall Configuration and Testing (UFW)

**Objective:** Configure and test basic firewall rules to allow or block traffic on Linux.

## Environment
- OS: Kali Linux (rolling)
- Tool: UFW (Uncomplicated Firewall) v0.36.2
- Shell: zsh

## Procedure

| Step | Command | Purpose |
|------|---------|---------|
| 1 | `sudo ufw --version` | Verify UFW installation |
| 2 | `sudo ufw status verbose` | List current firewall rules |
| 3 | `sudo ufw status numbered` | List rules with index numbers |
| 4 | `sudo ufw deny 23/tcp` | Block inbound Telnet traffic |
| 5 | `timeout 5 nc -zv localhost 23` | Test the block rule |
| 6 | `sudo ufw allow 22/tcp` | Allow inbound SSH traffic |
| 7 | `sudo ufw delete deny 23/tcp` | Remove the test block rule |
| 8 | `sudo ufw status verbose` | Confirm final rule set |

## Final Rule Set

Status: active
Default: deny (incoming), allow (outgoing), disabled (routed)

To Action From

22/tcp ALLOW IN Anywhere
22/tcp (v6) ALLOW IN Anywhere (v6)

## Screenshots

| File | Description |
|------|-------------|
| `01-ufw-status-and-numbered.png` | UFW version and initial rule listing |
| `02-block-telnet-and-test.png` | Telnet (23/tcp) blocked; connection test refused |
| `03-allow-ssh-and-remove-block.png` | SSH allowed; Telnet block removed |
| `04-final-state.png` | Final active rule set |

## How a Firewall Filters Traffic

A firewall inspects each packet's source/destination IP, port, protocol, and connection state, then matches it against an ordered rule list. The first matching rule determines the action. UFW's default policy here denies all inbound traffic and permits outbound. Stateful inspection automatically allows replies to outbound connections. Rules apply separately to IPv4/IPv6 and to inbound, outbound, or routed directions.

## Outcome

Successfully configured UFW to block Telnet (23/tcp), verified the block, allowed SSH (22/tcp), and restored the original state by removing the test rule. Demonstrated practical firewall management and network traffic filtering.
