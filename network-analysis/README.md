
# Network Traffic Analysis

## Overview
Used Wireshark to capture and analyze network traffic between lab machines,
identifying an unencrypted file transfer that exposed credentials and file
contents in plaintext.

---

## Setup
A basic FTP server (vsftpd) was configured on a Kali Linux machine to receive
a file transfer from a Windows machine, while Wireshark captured the traffic
on the wire.

![Apache/FTP server status](./screenshots/figure5-apache-web-server-status.png)

![Configuring the FTP server](./screenshots/figure12.1-configure-ftp-server.png)

## File Transfer
A file was transferred from the Windows machine to the Linux FTP server using
FileZilla, simulating a data exfiltration scenario.

![FileZilla FTP transfer](./screenshots/figure12.2-filezilla-ftp-transfer.png)

## Packet Capture Analysis
With the Wireshark display filter `ftp`, the capture showed the full FTP
session in plaintext — including the `STOR` command, the filename, and the
transfer confirmation. Because FTP is unencrypted, this traffic (and the
credentials used to authenticate) would be fully readable to anyone
positioned to intercept it on the network.

![Wireshark FTP capture](./screenshots/figure12.3-wireshark-ftp-capture.png)

## Findings
- FTP transmits both credentials and file contents unencrypted — trivially
  interceptable with a basic packet capture
- This kind of traffic is a strong Indicator of Compromise (IoC) when seen
  going to an unfamiliar or external host
- Filtering by protocol (`ftp`, `http`, `dns`, etc.) in Wireshark is the
  fastest way to isolate relevant traffic in a larger capture

## Recommendation
Replace FTP with an encrypted alternative (SFTP/FTPS) for any file transfer
involving sensitive data, and monitor for outbound connections on
unencrypted file-transfer ports.

## Screenshots
Screenshots of the VM setup and configuration are included in the `/screenshots` folder.

