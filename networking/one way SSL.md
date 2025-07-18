
step 1: get your modem's ip address by using :
--------->>>>>     curl ifconfig.me

step 2: set class A (ipv4) record in dns setting of the domain you bought . Set the modem's ip in ipv4 address . 

step 3: brew install certbot 

step 4: sudo certbot -d "*.akshitaskosmos.dev" --manual --preferred-challenges dns certonly

to generate a certificate from a trusted CA (lets's encrypt)

step 5: it will generate a key which you will configure as TXT class in your dns settings for your domain giving it the name ("_acme-challenge.akshitaskosmos.dev") 

step 6: then it will generate a valid certificate with fullchain.pem and privkey.pem files which you will store in the /tmp 

