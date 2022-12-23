# Nmap

Below is a quick summary of the command-line options for Nmap.

| Scan Type              | Example Command                             |
| ---------------------- | ------------------------------------------- |
| ARP Scan               | `sudo nmap -PR -sn MACHINE_IP/24`           |
| ICMP Echo Scan         | `sudo nmap -PE -sn MACHINE_IP/24`           |
| ICMP Timestamp Scan    | `sudo nmap -PP -sn MACHINE_IP/24`           |
| ICMP Address Mask Scan | `sudo nmap -PM -sn MACHINE_IP/24`           |
| TCP SYN Ping Scan      | `sudo nmap -PS22,80,443 -sn MACHINE_IP/30`  |
| TCP ACK Ping Scan      | `sudo nmap -PA22,80,443 -sn MACHINE_IP/30`  |
| UDP Ping Scan          | `sudo nmap -PU53,161,162 -sn MACHINE_IP/30` | 

Remember to add `-sn` if you are only interested in host discovery without port-scanning. Omitting `-sn` will let Nmap default to port-scanning the live hosts.

| Option | Purpose                          |
| ------ | -------------------------------- |
| -n     | no DNS lookup                    |
| -R     | reverse-DNS lookup for all hosts |
| -sn    | host discovery only              | 

Types of scans

| Port Scan Type                 | Example Command                                       |
| ------------------------------ | ----------------------------------------------------- |
| TCP Connect Scan               | `nmap -sT MACHINE_IP`                                 |
| TCP SYN Scan                   | `sudo nmap -sS MACHINE_IP`                            |
| UDP Scan                       | `sudo nmap -sU MACHINE_IP`                            |
| TCP Null Scan                  | `sudo nmap -sN MACHINE_IP`                            |
| TCP FIN Scan                   | `sudo nmap -sF MACHINE_IP`                            |
| TCP Xmas Scan                  | `sudo nmap -sX MACHINE_IP`                            |
| TCP Maimon Scan                | `sudo nmap -sM MACHINE_IP`                            |
| TCP ACK Scan                   | `sudo nmap -sA MACHINE_IP`                            |
| TCP Window Scan                | `sudo nmap -sW MACHINE_IP`                            |
| Custom TCP Scan                | `sudo nmap --scanflags URGACKPSHRSTSYNFIN MACHINE_IP` |
| Spoofed Source IP              | `sudo nmap -S SPOOFED_IP MACHINE_IP`                  |
| Spoofed MAC Address            | `--spoof-mac SPOOFED_MAC`                             |
| Decoy Scan                     | `nmap -D DECOY_IP,ME MACHINE_IP`                      |
| Idle (Zombie) Scan             | `sudo nmap -sI ZOMBIE_IP MACHINE_IP`                  |
| Fragment IP data into 8 bytes  | `-f`      |                                           
| Fragment IP data into 16 bytes | `-ff`                                               |

These scan types should get you started discovering running TCP and UDP services on a target host.

| Option                  | Purpose                                  |
| ----------------------- | ---------------------------------------- |
| `-p-`                   | all ports                                |
| `-p1-1023`              | scan ports 1 to 1023                     |
| `-F`                    | 100 most common ports                    |
| `-r`                    | scan ports in consecutive order          |
| `-T<0-5>`               | -T0 being the slowest and T5 the fastest |
| `--max-rate 50`         | rate <= 50 packets/sec                   |
| `--min-rate 15`         | rate >= 15 packets/sec                   |
| `--min-parallelism 100` | at least 100 probes in parallel          |
| `--reason`              | explains how Nmap made its conclusion    |
| `-v`                    | verbose                                  |
| `-vv`                   | very verbose                             |
| `-d`                    | debugging                                |
| `-dd`                   | more details for debugging               | 






#tools #nmap