PORT     STATE SERVICE       REASON          VERSION
80/tcp   open  http          syn-ack ttl 127 Microsoft IIS httpd 10.0
|_http-generator: Nicepage 5.0.7, nicepage.com
|_http-server-header: Microsoft-IIS/10.0
| http-methods: 
|   Supported Methods: OPTIONS TRACE GET HEAD POST
|_  Potentially risky methods: TRACE
|_http-title: Home
81/tcp   open  http          syn-ack ttl 127 Microsoft IIS httpd 10.0
|_http-title: IIS Windows
| http-methods: 
|   Supported Methods: OPTIONS TRACE GET HEAD POST
|_  Potentially risky methods: TRACE
|_http-server-header: Microsoft-IIS/10.0
3389/tcp open  ms-wbt-server syn-ack ttl 127 Microsoft Terminal Services
|_ssl-date: 2024-02-28T05:07:09+00:00; +2s from scanner time.
| rdp-ntlm-info: 
|   Target_Name: OSCP
|   NetBIOS_Domain_Name: OSCP
|   NetBIOS_Computer_Name: OSCP
|   DNS_Domain_Name: OSCP
|   DNS_Computer_Name: OSCP
|   Product_Version: 10.0.19041
|_  System_Time: 2024-02-28T05:07:03+00:00
| ssl-cert: Subject: commonName=OSCP
| Issuer: commonName=OSCP
| Public Key type: rsa
| Public Key bits: 2048
| Signature Algorithm: sha256WithRSAEncryption
| Not valid before: 2024-02-27T03:04:24
| Not valid after:  2024-08-28T03:04:24
| MD5:   6181:7169:dc30:3134:4553:4c2a:ffc6:3b61
| SHA-1: a38e:a2a2:3ba4:7c05:5044:d514:afa1:902a:64cf:f2f0
| -----BEGIN CERTIFICATE-----
| MIICzDCCAbSgAwIBAgIQGCcgMswcdZZDr0J9lTPyHDANBgkqhkiG9w0BAQsFADAP
| MQ0wCwYDVQQDEwRPU0NQMB4XDTI0MDIyNzAzMDQyNFoXDTI0MDgyODAzMDQyNFow
| DzENMAsGA1UEAxMET1NDUDCCASIwDQYJKoZIhvcNAQEBBQADggEPADCCAQoCggEB
| AOCD4WuS09gLS0rezhzygyUZLcayAMfoCTUq6YxbCo9DD49x0dyvfLyZ5zQjIbPX
| nMMh3Sy4Q7Jm2hG3qOFixEG5XUQlQX035Ao2V5DfTZzbL1tZwYZcpVziZvAcOxg6
| YV2HX2OvJbBgD0yJz0wUKvTor6HwajYkUXqFMFMZy9BROGTi+uEpVnkEhsmxNI10
| c4p1jP5Aci/xF1EWdXSrfFa5lUFuX2I3oGmxR1HiGqhrokofH6vSHcgU8ZAC+gBH
| ZWE1/hTDfzoKRmxhOKdBXrNQMFiwBdjtptSrTrAfu2GcjkHhz7hegmFgF4IAeC/g
| U9ktEmUICg8ZAwsQPNYpx4UCAwEAAaMkMCIwEwYDVR0lBAwwCgYIKwYBBQUHAwEw
| CwYDVR0PBAQDAgQwMA0GCSqGSIb3DQEBCwUAA4IBAQAR8h28JpazadD+lHQFEfyw
| HrafgRhmKi8/Fuj6g7PeI8swSynrCNJTIM/ubAlvVv1a8vbqmAeAyDZqvXU9IGrq
| /5/+rt1D4/HTNpcHRb5oRCOZOPnKOXkfvgcatD2/Tck8obkkCfaROH+lDCYysiq/
| I4a95umwKODOQqv/WUnlU5p7oA7PeR2+cEpZb5AYuDx2sTupw9Es1hkXPZ/GG2Ya
| guwYh0HMYcqV0Qi+y98sbhpP2kADn26oG/04qKMaaM+FJkrvIHYFPc0/1IODoCvg
| jGk8LPLIwt4o7XPVTu2rNO4OkzIMFVPnAaXTMtG+5bkvc/go7POPNgUQnh4klgA8
|_-----END CERTIFICATE-----
8000/tcp open  http-alt      syn-ack ttl 127 WSGIServer/0.2 CPython/3.10.4
|_http-server-header: WSGIServer/0.2 CPython/3.10.4
| fingerprint-strings: 
|   FourOhFourRequest: 
|     HTTP/1.1 404 Not Found
|     Date: Wed, 28 Feb 2024 05:01:56 GMT
|     Server: WSGIServer/0.2 CPython/3.10.4
|     Content-Type: text/html
|     X-Frame-Options: DENY
|     Content-Length: 5124
|     X-Content-Type-Options: nosniff
|     Referrer-Policy: same-origin
|     Cross-Origin-Opener-Policy: same-origin
|     <!DOCTYPE html>
|     <html lang="en">
|     <head>
|     <meta http-equiv="content-type" content="text/html; charset=utf-8">
|     <title>Page not found at /nice ports,/Trinity.txt.bak</title>
|     <meta name="robots" content="NONE,NOARCHIVE">
|     <style type="text/css">
|     html * { padding:0; margin:0; }
|     body * { padding:10px 20px; }
|     body * * { padding:0; }
|     body { font:small sans-serif; background:#eee; color:#000; }
|     body>div { border-bottom:1px solid #ddd; }
|     font-weight:normal; margin-bottom:.4em; }
|     span { font-size:60%; color:#666; font-weight:normal; }
|     table { border:none; border-collapse: collapse;
|   GetRequest: 
|     HTTP/1.1 302 Found
|     Date: Wed, 28 Feb 2024 05:01:50 GMT
|     Server: WSGIServer/0.2 CPython/3.10.4
|     Content-Type: text/html; charset=utf-8
|     Location: /login?next=/
|     X-Frame-Options: DENY
|     Content-Length: 0
|     Vary: Cookie
|     X-Content-Type-Options: nosniff
|     Referrer-Policy: same-origin
|     Cross-Origin-Opener-Policy: same-origin
|   Socks5: 
|     <!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN"
|     "http://www.w3.org/TR/html4/strict.dtd">
|     <html>
|     <head>
|     <meta http-equiv="Content-Type" content="text/html;charset=utf-8">
|     <title>Error response</title>
|     </head>
|     <body>
|     <h1>Error response</h1>
|     <p>Error code: 400</p>
|     <p>Message: Bad request syntax ('
|     ').</p>
|     <p>Error code explanation: HTTPStatus.BAD_REQUEST - Bad request syntax or unsupported method.</p>
|     </body>
|_    </html>
| http-title: File Management System
|_Requested resource was /login?next=/
| http-methods: 
|_  Supported Methods: GET HEAD OPTIONS
1 service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at https://nmap.org/cgi-bin/submit.cgi?new-service :
SF-Port8000-TCP:V=7.94SVN%I=9%D=2/28%Time=65DEBE3C%P=x86_64-pc-linux-gnu%r
SF:(GetRequest,143,"HTTP/1\.1\x20302\x20Found\r\nDate:\x20Wed,\x2028\x20Fe
SF:b\x202024\x2005:01:50\x20GMT\r\nServer:\x20WSGIServer/0\.2\x20CPython/3
SF:\.10\.4\r\nContent-Type:\x20text/html;\x20charset=utf-8\r\nLocation:\x2
SF:0/login\?next=/\r\nX-Frame-Options:\x20DENY\r\nContent-Length:\x200\r\n
SF:Vary:\x20Cookie\r\nX-Content-Type-Options:\x20nosniff\r\nReferrer-Polic
SF:y:\x20same-origin\r\nCross-Origin-Opener-Policy:\x20same-origin\r\n\r\n
SF:")%r(FourOhFourRequest,1518,"HTTP/1\.1\x20404\x20Not\x20Found\r\nDate:\
SF:x20Wed,\x2028\x20Feb\x202024\x2005:01:56\x20GMT\r\nServer:\x20WSGIServe
SF:r/0\.2\x20CPython/3\.10\.4\r\nContent-Type:\x20text/html\r\nX-Frame-Opt
SF:ions:\x20DENY\r\nContent-Length:\x205124\r\nX-Content-Type-Options:\x20
SF:nosniff\r\nReferrer-Policy:\x20same-origin\r\nCross-Origin-Opener-Polic
SF:y:\x20same-origin\r\n\r\n<!DOCTYPE\x20html>\n<html\x20lang=\"en\">\n<he
SF:ad>\n\x20\x20<meta\x20http-equiv=\"content-type\"\x20content=\"text/htm
SF:l;\x20charset=utf-8\">\n\x20\x20<title>Page\x20not\x20found\x20at\x20/n
SF:ice\x20ports,/Trinity\.txt\.bak</title>\n\x20\x20<meta\x20name=\"robots
SF:\"\x20content=\"NONE,NOARCHIVE\">\n\x20\x20<style\x20type=\"text/css\">
SF:\n\x20\x20\x20\x20html\x20\*\x20{\x20padding:0;\x20margin:0;\x20}\n\x20
SF:\x20\x20\x20body\x20\*\x20{\x20padding:10px\x2020px;\x20}\n\x20\x20\x20
SF:\x20body\x20\*\x20\*\x20{\x20padding:0;\x20}\n\x20\x20\x20\x20body\x20{
SF:\x20font:small\x20sans-serif;\x20background:#eee;\x20color:#000;\x20}\n
SF:\x20\x20\x20\x20body>div\x20{\x20border-bottom:1px\x20solid\x20#ddd;\x2
SF:0}\n\x20\x20\x20\x20h1\x20{\x20font-weight:normal;\x20margin-bottom:\.4
SF:em;\x20}\n\x20\x20\x20\x20h1\x20span\x20{\x20font-size:60%;\x20color:#6
SF:66;\x20font-weight:normal;\x20}\n\x20\x20\x20\x20table\x20{\x20border:n
SF:one;\x20border-collapse:\x20collapse;\x20")%r(Socks5,213,"<!DOCTYPE\x20
SF:HTML\x20PUBLIC\x20\"-//W3C//DTD\x20HTML\x204\.01//EN\"\n\x20\x20\x20\x2
SF:0\x20\x20\x20\x20\"http://www\.w3\.org/TR/html4/strict\.dtd\">\n<html>\
SF:n\x20\x20\x20\x20<head>\n\x20\x20\x20\x20\x20\x20\x20\x20<meta\x20http-
SF:equiv=\"Content-Type\"\x20content=\"text/html;charset=utf-8\">\n\x20\x2
SF:0\x20\x20\x20\x20\x20\x20<title>Error\x20response</title>\n\x20\x20\x20
SF:\x20</head>\n\x20\x20\x20\x20<body>\n\x20\x20\x20\x20\x20\x20\x20\x20<h
SF:1>Error\x20response</h1>\n\x20\x20\x20\x20\x20\x20\x20\x20<p>Error\x20c
SF:ode:\x20400</p>\n\x20\x20\x20\x20\x20\x20\x20\x20<p>Message:\x20Bad\x20
SF:request\x20syntax\x20\('\\x05\\x04\\x00\\x01\\x02\\x80\\x05\\x01\\x00\\
SF:x03'\)\.</p>\n\x20\x20\x20\x20\x20\x20\x20\x20<p>Error\x20code\x20expla
SF:nation:\x20HTTPStatus\.BAD_REQUEST\x20-\x20Bad\x20request\x20syntax\x20
SF:or\x20unsupported\x20method\.</p>\n\x20\x20\x20\x20</body>\n</html>\n");
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
OS fingerprint not ideal because: Missing a closed TCP port so results incomplete
