##To renew certificate for Let's Encrypt

1. Restart the server (if using Bitnami  + Apache2). Apache reads existing certificate only on startup.
> sudo /opt/bitnami/ctlscript.sh restart apache

2. Add domain names as Environment Variables
> DOMAIN=example.com

3. Add wildcard domain name as Environment Variable
> WILDCARD=*.$DOMAIN

4. Validate that environment variables have been set.
> echo $DOMAIN && echo $WILDCARD

5. Start the interactive Certbot process
> sudo certbot -d $DOMAIN -d $WILDCARD --manual --preferred-challenges dns certonly

6. Press Y when requested for IP Logging( this is a must to use Certbot). Enter email address if prompted
> Y

7. Deploy the given DNS TXT file (use tool like https://dnschecker.org to confirm that DNS setting has been propagated)
e.g. HOSTNAME: _acme-challenge.example.com
e.g. VALUE: HrYajiacTgO00aEkShsSokDbd-Q7WndkkD_skRb275w

8. If given a second DNS TXT record, make sure to replace the current DNS TXT record and wait for propagation with the new value setting.

9. Press ENTER to continue.

10. Restart the server to activate the new certification
> sudo /opt/bitnami/ctlscript.sh restart apache

11. Check site to see if SSL cert has been updated.

Certbot certification only lasts for 3 months. This process of renewal can be triggered at any time.

For reference:
https://lightsail.aws.amazon.com/ls/docs/en_us/articles/amazon-lightsail-using-lets-encrypt-certificates-with-wordpress#request-a-lets-encrypt-certificate-wordpress
