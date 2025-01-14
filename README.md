![image](https://github.com/user-attachments/assets/57f8896d-6803-4f6a-ba6b-eddd67f57d48)![image](https://github.com/user-attachments/assets/b223301f-09e5-462f-9eea-f786c1703551)![image](https://github.com/user-attachments/assets/b1ba26ed-2f35-40f0-8ba4-02cb96834158)![image](https://github.com/user-attachments/assets/323c8b6e-8e21-4665-a160-7f62d6a5fc21)![image](https://github.com/user-attachments/assets/19d5e2b3-01a0-4dea-bb38-17270dbdc8e2)![image](https://github.com/user-attachments/assets/ddaa5cdb-fd75-4c90-8efd-6d2b9ddfe1d0)![image](https://github.com/user-attachments/assets/453a0877-a03a-46c0-b8e7-a8daf50b187a)# docker_metasploit_metasploitable2
[docker_link](https://medium.com/@habibsemouma/setting-up-metasploitable2-and-kali-in-docker-for-pentesting-6b71a089c4a2)
* search metasploitable2
```
docker search metasploitable
```
* pull (download metasploitable2)
```
docker pull tleemcjr/metasploitable2
```
* pull (download kali linux)
```
docker pull kalilinux/kali-rolling
```
* Test if image is present :
```
docker images
```
* Creation of network for the victim and the pentester
```
docker network create pentest
```
* RUNING on TERMINAL 1 (victim : metasploitable 2) :
```
sudo docker run --network=pentest -h victim -it --rm --name metasploitable2 tleemcjr/metasploitable2
```
Finding ip on victim : 
```
ip a
```
* RUNING on TERMINAL 2 (pentester : kali linux)
```
sudo docker run --network=pentest -h attacker -it --rm --name kalibox kalilinux/kali-rolling
```
Installing first tools : 
```
apt update
apt install net-tools
apt install nmap
ifconfig
apt install -y iputils-ping
apt install metasploit-framework
```
* Testing ping for 2 machines 
```
ping <ip_victim>
```
```
ping <ip_pentester>
```
* Testing nmap roadmap 
```
nmap -F <ip_victim>
```
* Finding host and scanning network 
learning.oreilly.com/library/view/ceh-certified-ethical

1. check for live systems
```
sudo nmap -sP <ip_victim_network>/24
```

2. check for open ports
(port 80, 443 for web)
```
sudo nmap -sT -p 80,443 10.7.1.0/24
```
T : for TCP using 3-way handshake (Full Open scan) </br>
message 1 : i'm prot 443 Are you theire (SYN) </br>
message 2 : yes i'm thiere, (SYN ACK) </br>
message 3 : let's talk (ACK) </br>
More detect by the IDS </br>
3-way handshake without connection 
```
sudo nmap -sS -p 80,443 <ip_victim_network>/24
```

S : Stealthy (half Open Scan)
(2way handshake)
```
sudo nmap -sT <ip_victim>
```
If with wirshark :  </br>
filter by ip.addr eq <ip_victim> </br>
click one converstation and "apply this filter" </br>

4. Perform banner grabbing
OS detection :
```
sudo nmap -sO <ip_victim>
```
Mora options 
```
sudo nmap -A <ip_victim>
```

5. scan vulnerabilities
```
namp --script vuln <ip_victim>
```
* Scanning using msfconsole :
In Kali Terminal :
```
msfconsole
```
```
show payloads 
```
```
use auxiliary/scanner/portscan/tcp
```
```
show options
```
```
set ports 80
```
```
set rhosts <ip_victim>
```
```
run
```
OR
```
exploit
```

