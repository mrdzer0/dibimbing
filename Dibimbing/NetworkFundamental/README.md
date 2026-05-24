# Cheatseet Network Fundamental Class

## Troubleshooting jaringan
```sh
# 1. Cek IP config
ip addr show           # Linux
ipconfig /all          # Windows

# 2. Test konektivitas layer 3
ping 127.0.0.1         # Loopback
ping 192.168.1.1       # Gateway
ping 8.8.8.8           # Internet IP

# 3. Test DNS
nslookup google.com
dig google.com

# 4. Trace rute
traceroute 8.8.8.8     # Linux
tracert 8.8.8.8        # Windows

# 5. Lihat routing table
ip route show          # Linux
route print            # Windows
```

## Network Commands Cheatsheet
```sh
# Linux / macOS
ip addr show        #Lihat IP address
ip route show       #Routing table
ping [host]         #Test konektivitas
traceroute [host]   #Lacak rute
netstat -tulnp      #Port yang aktif
ss -tulnp           #Socket statistics
dig [domain]        #DNS query
arp -n              #ARP table

# Windows
ipconfig /all       #IP config lengkap
ping [host]         #Test konektivitas
tracert [host]      #Lacak rute
netstat -an         #Koneksi aktif
nslookup [domain]   #DNS query
arp -a              #ARP table
route print         #Routing table
getmac              #MAC addresses

# Cisco IOS
show ip int brief       #Status interface
show ip route           #Routing table
show arp                #ARP table
show vlan brief         #VLAN info
show mac address-table  #MAC table switch
ping [ip]               #Test ping
debug ip packet         #Debug packet
show run                #Konfigurasi aktif
```

## Another Reference
### Book
- Computer Networks - Andrew S. Tanenbaum
- TCP/IP Illustrated Vol.1 - W. Stevens
- Network Warrior - Gary A. Donahue
- Cisco CCNA Study Guide

### Online Platform
- Cisco NetAcad (netacad.com)
- Udemy - Networking courses
- TryHackMe - Networking challenges

### Practice Labs
- Cisco Packet Tracer
- GNS3 - Open source network simulator

### YouTube Channels
- NetworkChuck [https://www.youtube.com/@NetworkChuck]
- Professor Messer [https://www.youtube.com/@professormesser]
- David Bombal [https://www.youtube.com/@davidbombal]