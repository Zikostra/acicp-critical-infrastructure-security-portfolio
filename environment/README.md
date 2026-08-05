# Controlled Two-VM Laboratory Environment

## Platform

- Host virtualisation: KVM/libvirt
- Guest operating system: Ubuntu Server 24.04 LTS
- Private network: 192.168.56.0/24
- Host bridge: 192.168.56.1

## Virtual Machines

| VM | IP address | Role |
|---|---|---|
| VM-A | 192.168.56.10 | Testing client and traffic generator |
| VM-B | 192.168.56.20 | TLS server and defensive inspection host |

## Important Limitation

The repository stores environment documentation and evidence only. It does not store VM disk images, passwords or private keys.
