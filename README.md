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

docker cp ejbca:/opt/keyfactor/secrets/persistent/tls/ejbca.besign.app/server.jks .
docker cp ejbca:/opt/keyfactor/secrets/persistent/tls/ejbca.besign.app/server.storepasswd .

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

## Add SuperAdmin

### Add Role Access

menu Roles and Access Roles
Add
X509: CN, Common name
CA: ManagementCA
Match Value: SuperAdmin2
Add

### Add End Entity

End Entity Profile: EMPTY
Username: superadmin2
Password (or Enrollment Code): tcr8b8Z4FXd8ZWIM3iOzAJoL
Confirm Password: tcr8b8Z4FXd8ZWIM3iOzAJoL
Batch generation (clear text pwd storage): Use
userid: c-0cpcnb7nuiqyrnjob
O, Organization: EJBCA Container Quickstart
CN, Common name: SuperAdmin2
Certificate Profile: ENDUSER
CA: ManagementCA
Token: P12 file
Add

### Download

goto RA Web https://192.168.1.150/ejbca/ra/enrollwithusername.xhtml
Username: superadmin2
Enrollment code: tcr8b8Z4FXd8ZWIM3iOzAJoL
RSA, 2,048-bit
Download JKS
