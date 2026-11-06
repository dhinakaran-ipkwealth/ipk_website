# IPK Wealth static website

This is a standalone static landing page for IPK Wealth Service Private
Limited. It uses the supplied IPK Wealth logo and the brand tagline found in
the `IPK_BO` web application.

## Deploy to the EC2 instance

1. Copy `index.html`, `styles.css`, and the `assets` directory to
   `/var/www/ipkwealth/` on the instance.
2. Install the Nginx site config:

   ```sh
   sudo cp nginx/ipkwealth.conf /etc/nginx/conf.d/ipkwealth.conf
   sudo nginx -t
   sudo systemctl reload nginx
   ```

3. Allow inbound TCP ports 80 and 443 in the EC2 security group.
4. Configure DNS A records for `ipkwealth.com` and `www.ipkwealth.com` to
   `15.252.231.55`.
5. After DNS resolves to the instance, install Certbot for your Linux
   distribution and run:

   ```sh
   sudo certbot --nginx -d ipkwealth.com -d www.ipkwealth.com
   ```

   Follow Certbot's prompts to enable HTTPS and redirect HTTP to HTTPS. The
   supplied Nginx config serves HTTP initially so certificate issuance can
   complete; Certbot will add the HTTPS listener.

The site files live at `/var/www/ipkwealth`. The Nginx config includes the
domain names and the instance IP so the page can also be opened by IP before
DNS or HTTPS is configured.
