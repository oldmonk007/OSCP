192.168.102.100 - entry point
	
	PORT      STATE SERVICE       REASON          VERSION
53/tcp    open  domain        syn-ack ttl 127 Simple DNS Plus
88/tcp    open  kerberos-sec  syn-ack ttl 127 Microsoft Windows Kerberos (server time: 2024-02-28 03:20:56Z)
135/tcp   open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
139/tcp   open  netbios-ssn   syn-ack ttl 127 Microsoft Windows netbios-ssn
389/tcp   open  ldap          syn-ack ttl 127 Microsoft Windows Active Directory LDAP (Domain: oscp.exam0., Site: Default-First-Site-Name)
445/tcp   open  microsoft-ds? syn-ack ttl 127
464/tcp   open  kpasswd5?     syn-ack ttl 127
593/tcp   open  ncacn_http    syn-ack ttl 127 Microsoft Windows RPC over HTTP 1.0
636/tcp   open  tcpwrapped    syn-ack ttl 127
3268/tcp  open  ldap          syn-ack ttl 127 Microsoft Windows Active Directory LDAP (Domain: oscp.exam0., Site: Default-First-Site-Name)
3269/tcp  open  tcpwrapped    syn-ack ttl 127
5985/tcp  open  http          syn-ack ttl 127 Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Not Found
9389/tcp  open  mc-nmf        syn-ack ttl 127 .NET Message Framing
49665/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
49666/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
49667/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
49669/tcp open  ncacn_http    syn-ack ttl 127 Microsoft Windows RPC over HTTP 1.0
49670/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
49673/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
49701/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
53027/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC20  ftp-data
	
		389/tcp open  ldap
| ldap-search: 
|   Context: DC=oscp,DC=exam; QFilter: users; Attributes: sAMAccountName
|     dn: CN=Guest,CN=Users,DC=oscp,DC=exam
|         sAMAccountName: Guest
|     dn: CN=lisa,CN=Users,DC=oscp,DC=exam
|         sAMAccountName: lisa
|     dn: CN=svc_sql,CN=Users,DC=oscp,DC=exam
|_        sAMAccountName: svc_sql

		
192.168.102.101

135/tcp   open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
139/tcp   open  netbios-ssn   syn-ack ttl 127 Microsoft Windows netbios-ssn
445/tcp   open  microsoft-ds? syn-ack ttl 127
5985/tcp  open  http          syn-ack ttl 127 Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-title: Not Found
|_http-server-header: Microsoft-HTTPAPI/2.0
8080/tcp  open  http          syn-ack ttl 127 Apache Tomcat 8.5.19
| http-methods: 
|_  Supported Methods: GET HEAD POST
|_http-favicon: Apache Tomcat
|_http-title: Apache Tomcat/8.5.19
49665/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
49666/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC

gobuster on 8080 with common and big no results

192.168.102.102

PORT      STATE SERVICE       REASON          VERSION
135/tcp   open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
139/tcp   open  netbios-ssn   syn-ack ttl 127 Microsoft Windows netbios-ssn
445/tcp   open  microsoft-ds? syn-ack ttl 127
1433/tcp  open  ms-sql-s      syn-ack ttl 127 Microsoft SQL Server 2019 15.00.2000.00; RTM
| ms-sql-ntlm-info: 
|   192.168.102.102:1433: 
|     Target_Name: oscp
|     NetBIOS_Domain_Name: oscp
|     NetBIOS_Computer_Name: MS02
|     DNS_Domain_Name: oscp.exam
|     DNS_Computer_Name: ms02.oscp.exam
|     DNS_Tree_Name: oscp.exam
|_    Product_Version: 10.0.17763
|_ssl-date: 2024-02-28T03:25:05+00:00; +2s from scanner time.
| ms-sql-info: 
|   192.168.102.102:1433: 
|     Version: 
|       name: Microsoft SQL Server 2019 RTM
|       number: 15.00.2000.00
|       Product: Microsoft SQL Server 2019
|       Service pack level: RTM
|       Post-SP patches applied: false
|_    TCP port: 1433
| ssl-cert: Subject: commonName=SSL_Self_Signed_Fallback
| Issuer: commonName=SSL_Self_Signed_Fallback
| Public Key type: rsa
| Public Key bits: 2048
| Signature Algorithm: sha256WithRSAEncryption
| Not valid before: 2024-01-17T19:18:13
| Not valid after:  2054-01-17T19:18:13
| MD5:   fbc5:7a53:862f:0b5b:ed91:f356:6648:a76b
| SHA-1: 4503:8be0:fcc4:b2f3:a15d:e1e2:fd61:608c:fd75:d9b2
| -----BEGIN CERTIFICATE-----
| MIIDADCCAeigAwIBAgIQbiVxxpfvuLVEZTFrKa+k7DANBgkqhkiG9w0BAQsFADA7
| MTkwNwYDVQQDHjAAUwBTAEwAXwBTAGUAbABmAF8AUwBpAGcAbgBlAGQAXwBGAGEA
| bABsAGIAYQBjAGswIBcNMjQwMTE3MTkxODEzWhgPMjA1NDAxMTcxOTE4MTNaMDsx
| OTA3BgNVBAMeMABTAFMATABfAFMAZQBsAGYAXwBTAGkAZwBuAGUAZABfAEYAYQBs
| AGwAYgBhAGMAazCCASIwDQYJKoZIhvcNAQEBBQADggEPADCCAQoCggEBAK7NbILh
| dBwvl469Deq6UFhtChDU9AP2ARb9GEg7LGEiSnNKvYC4Bx0BsPv4aCXUGoOK/p5a
| ihfQEjl3u1xZuQf3J8z87CUaF2rZWa78G9YrEVR0DjDyN6i7HL8H6ByCpxL1m70c
| UZNq0LkFZSyGAZajQKL8y+po+kmAu19Ly7e1olV2JeVUm446gQBENrj92Fsi0Uio
| shyKyZ6CSNsRPZL7Fuvfh7H5QgeHwEEcrsjRM0wh+RR/pO5eGB/v655UFy5AZld6
| OA8UF/xfrXtOSinkoZurPd4XYuWdvOL47bxIOR38w0vpR8HQoVdhdkzl6NddTmpd
| KmcyIyz1yevxs+kCAwEAATANBgkqhkiG9w0BAQsFAAOCAQEAFpvex/WwDYAm9t4t
| O8MZmS9BgdkTiH5auqyV1ZL6jFsif4Hi+GxXWVfxpbJKTYcPTo90bxugN3Pa90Ad
| H8H7f/kKjCEV/Aua02Y/7iBx5JiDe2U/zKNwbtzXVZTlPgEMzk41usCO/mP+NvXe
| PoZK4VeB4r4za3hdz/yWlkgGoJBgo8tsqvWROH54DYfth+TfHD+B9pXzR/s4K+2U
| Dh6EvHIuiUpuxnS7WEVHGLyGTHRibUpJSeFqKVfpc3PXKiVkJnuf1WtFwhfj94k2
| 9kfrd2s+txaXxJvBctz7th/DtNqpdeg+pPH410qDF7S2lZ+6BVvrorKz07sHd08I
| G78nYA==
|_-----END CERTIFICATE-----
5985/tcp  open  http          syn-ack ttl 127 Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Not Found
49665/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
49666/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC

