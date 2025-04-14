# odoo-iot
All related to the IoT setup

1. Odoo Knowledge IOT Structure and more: 
===
https://lse-odoo.github.io/iot/index.html


2.Odoo Nightly builds
===================
https://nightly.odoo.com/


===
3.🔐 Crear un certificado autofirmado para la IoT Box de Odoo
📌 Fuente oficial: 
Odoo Forum(https://www.odoo.com/es/forum/ayuda-1/https-connection-to-iot-box-failed-170398)
===
📋 Instrucciones:

Conéctate a tu IoT Box.

Crea un archivo de configuración para OpenSSL:
cat << 'EOT' > /etc/ssl/san.cnf
[req]
default_bits  = 2048
distinguished_name = req_distinguished_name
req_extensions = req_ext
x509_extensions = v3_req
prompt = no

[req_distinguished_name]
countryName = XX
stateOrProvinceName = N/A
localityName = N/A
organizationName = YourName
commonName = OdooIoTBoxCertificate

[req_ext]
subjectAltName = @alt_names

[v3_req]
subjectAltName = @alt_names

[alt_names]
IP.1 = YOUR_IOTBOX_IP
EOT
🔁 Reemplaza YOUR_IOTBOX_IP por la IP real de tu IoT Box.
===
Ejecuta el siguiente comando para generar el certificado:

openssl req -x509 -nodes -days 365000 -newkey rsa:2048 -keyout key.pem -out cert.pem -config /etc/ssl/san.cnf

4.Mueve el certificado al directorio adecuado (ejemplo):

mv cert.pem /etc/ssl/certs/
mv key.pem /etc/ssl/private/

5.Configura Nginx para usar este certificado.



