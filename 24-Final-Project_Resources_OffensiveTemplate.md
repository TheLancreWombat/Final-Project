# Red Team: Summary of Operations

## Table of Contents
- Exposed Services
- Critical Vulnerabilities
- Exploitation

### Exposed Services

Nmap scan results for each machine reveal the below services and OS details:

```bash
$ nmap -sV -A 192.168.1.110

```

This scan identifies the services below as potential points of entry:
- Target 1
  22/tcp OpenSSH 6.7p1
  80/tcp Apache httpd 2.4.10
  111/tcp rpcbind
  139/tcp Samba smbd 3.X-4.X
  445/tcp Samba smbd 4.2.14-Debian

The following vulnerabilities were identified on each target:
- Target 1
  - CVE-2015-5600
  - EBD-ID:40888
  - EBD-ID:41173
  - CWE-200
  - CWE-521

_TODO: Include vulnerability scan results to prove the identified vulnerabilities._

### Exploitation
_TODO: Fill out the details below. Include screenshots where possible._

The Red Team was able to penetrate `Target 1` and retrieve the following confidential data:
- Target 1
  - `flag1.txt`: b9bbcb33e11b80be759c4e844862482d
    ### CWE-200
      - CWE-200 Information disclosure
        - Went to target1 website 192.168.1.110 and browserd source code of each page there
        - Ctrl+U to view source code
        - Ctrl+F 'flag'
  
  - `flag2.txt`: fc3fd58dcdad9ab23faca6e9a36e581c
    ### CWE-521
      - CWE-521 Weak Password Requirements
        - First used wpscan -e --url http://192.168.1.110/wordpress/ to enumerate usernames
        - Found usernames michael and steven 
        - ssh michael@192.168.1.110 then guessed michael as password to gain access to system
        - find / -name flag2.txt
