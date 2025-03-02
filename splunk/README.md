# How to create and sign your own TLS certificates

https://docs.splunk.com/Documentation/Splunk/9.3.1/Security/Howtoself-signcertificates

## Create the root certificate authority certificate

export SPLUNK_HOME=/opt/splunk
$SPLUNK_HOME/bin/splunk cmd openssl genrsa -aes256 -out myCertAuthPrivateKey.key 2048
$SPLUNK_HOME/bin/splunk cmd openssl req -new -key myCertAuthPrivateKey.key -out myCertAuthCertificate.csr
$SPLUNK_HOME/bin/splunk cmd openssl x509 -req -in myCertAuthCertificate.csr -sha512 -signkey myCertAuthPrivateKey.key -CAcreateserial -out myCertAuthCertificate.pem -days 1095

## Create server certificates and sign them with the root certificate authority certificate

$SPLUNK_HOME/bin/splunk cmd openssl genrsa -aes256 -out myServerPrivateKey.key 2048
$SPLUNK_HOME/bin/splunk cmd openssl req -new -key myServerPrivateKey.key -out myServerCertificate.csr
$SPLUNK_HOME/bin/splunk cmd openssl x509 -req -in myServerCertificate.csr -SHA256 -CA myCertAuthCertificate.pem -CAkey myCertAuthPrivateKey.key -CAcreateserial -out myServerCertificate.pem -days 1095

# How to prepare TLS certificates for use with the Splunk platform

https://docs.splunk.com/Documentation/Splunk/9.3.1/Security/HowtoprepareyoursignedcertificatesforSplunk

cat myServerCertificate.pem myServerPrivateKey.key myCertAuthCertificate.pem > combinedServerCertificate.pem

# Configure Splunk docker instance

https://splunk.github.io/docker-splunk/ADVANCED.html#usage

# default.yaml documentation

https://splunk.github.io/docker-splunk/ADVANCED.html#create-custom-configs
