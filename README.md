# network

`sudo netplan apply`
`sudo netplan try`
`sudo journalctl -u systemd-networkd`
`ip a`

# ejbca

`sudo docker compose up -d`
`sudo docker compose logs -f`
`sudo docker compose restart -d`
`sudo docker compose down`

key in /opt/keyfactor/secrets/server.\*
`keytool -importkeystore -srckeystore server.jks -destkeystore server.p12 -srcstoretype JKS -deststoretype PKCS12`

import key keychain (macos)

https://192.168.1.122:8443/ejbca/adminweb/ (if not work restart)

truststore in /opt/wildfly-\*/standalone/configuration/truststore.jks and password in standalone.xml (search "truststore.jks")

## Certificate Profiles (beSIGN)

Use Certificate Storage [?] : Use
Store Certificate Data [?] : Use
Basic Constraints : Use, Critical
Authority Key ID : Use
Subject Key ID : Use
CRL Distribution Points [?] : Use
Use CA defined CRL Distribution Point : Use
Authority Information Access : Use
Use CA defined OCSP locator : Use
Use CA defined CA issuer : Use

## Certification Authorities (beSIGN)

Enforce unique public keys [?] : Enforce
Enforce unique DN [?] :
Enforce unique Subject DN SerialNumber [?] : Enforce
Use Certificate Request History [?] : Use
Use User Storage [?] : Use
Use Certificate Storage [?] : Use
Default CA defined validation data => Generate All

## End Entity Profile (beSIGN)

Subject DN Attributes : CN, Common name. // Add
check Required, Modifiable
Subject Alternative Name [?]: RFC 822 Name (e-mail address) // Add
check Use entity e-mail field
