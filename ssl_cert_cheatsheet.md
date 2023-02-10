## SSL Certificate Cheatsheet ##
A cheatsheet to help guide through how to support SSL and identify/verify SSL certificates. This is not a full guide to explain everything yet.

### Shortcuts ###
How to display a cert
* Display a cert (does not display full chain): openssl x509 -in trustedCA.crt -text -noout
* Display a cert (including the full chain): openssl storeutl -noout -text -certs <cert_name>.

How to verify matching keys for certificate and private key
* openssl x509 -noout -modulus -in trustedCA.crt | openssl md5
* openssl rsa -noout -modulus -in private.key | openssl md5

How to add a certificate (Debian)
1. sudo cp <cert_name> /usr/local/share/ca-certificates/
2. sudo update-ca-certificates

How to remove a certificate (Debian)
1. Remove the files that were added to /usr/local/share/ca-certificates/
2. sudo update-ca-certificates -f (This basically just removes the symlinks that are unused)

Test that certificates are working on your system: `openssl s_client -connect <domain_name>:443`. If you don't have the certificates added yet, you can also use -CAfile option
if the cert is stored somewhere.




### Other Notes ###
* If setting up TLS on a server and you care about DNS, you must check in the cert that “Subject Alternative Name” and CN match a domain name.
*   

### Resources ###
* Beginner guide to certificates - https://www.youtube.com/watch?v=VH4gXcvkmOY&t=696s
* Splitting a cert up - https://stackoverflow.com/questions/3777075/ssl-certificate-rejected-trying-to-access-github-over-https-behind-firewall/4454754#4454754
* TODO: Example showing adding TLS configuration to Nginx