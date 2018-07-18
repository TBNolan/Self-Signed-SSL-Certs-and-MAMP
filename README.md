#1 Create req.conf
[req]
distinguished_name = req_distinguished_name
x509_extensions = v3_req
prompt = no
[req_distinguished_name]
C = US
ST = VA
L = SomeCity
O = MyCompany
OU = MyDivision
CN = www.company.com
[v3_req]
keyUsage = keyEncipherment, dataEncipherment
extendedKeyUsage = serverAuth
subjectAltName = @alt_names
[alt_names]
DNS.1 = www.company.net
DNS.2 = company.com
DNS.3 = company.net

#2 Generate cert.key
openssl genrsa -out cert.key 3072 -nodes

#3 Generate cert.crt
openssl req -new -x509 -key cert.key -sha256 -config req.conf -out cert.crt -days 730

#4 Load cert.crt into keychain and always trust
