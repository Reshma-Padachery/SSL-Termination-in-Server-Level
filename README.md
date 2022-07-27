# SSL-Termination-in-Server-Level for Self Signed  Certificates

Steps to be followed:

1)Check if apache httpd is installed in EC2 machine

2)Check for mod_ssl in cd /etc/httpd/modules,if not install using  ---3rd part module to integrate apache httpd with ssl
  yum install mod_ssl -y
  
3)check for openssl if installed,if not  ---package to create SSL certificate
  yum install openssl -y
  
 4)check if ssl.conf is created under cd /etc/httpd/conf.d after installation of mod_ssl
 
 5)Create a directory ssl under cd /etc/httpd
 
 
 
 Three Steps for Self Signed Certificate
 
 1)Key Generation
   openssl genrsa -out bulletclub.key 2048
   
  2)Create a certificate request
   openssl req -new  -key bulletclub -out bulletclub.csr 
   
   Give the  server hostname as www.bulletclub123.com
   
  3)Create a self signed certificate
  openssl x509 -req -days 365 -in bulletclub.csr –signkey bulletclub.key -out bulletclub.crt
  
6)Validate the certificate generated

      openssl x509 -in bulletclub.crt -text -noout
      
7)Go to cd /etc/httpd/conf.d/ssl.conf

    Edit at 4 places:
        * DocumentRoot /var/www/html
        * ServerName www.bulletclub123.com
        * SSLCertificateKeyPath
          /etc/httpd/ssl/...key
        *SSLCertificateFile
          /etc/httpd/ssl/...crt
8)Ensure that port 443 is open in security group
9)Export the certificate.
