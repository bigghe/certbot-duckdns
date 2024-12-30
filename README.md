# certbot-duckdns
Certbot manual DNS challenge for DuckDNS

#### Requirements:
- certbot
- curl
- cron (recommended)

#### Setup:
1. Clone repository
2. Write DuckDNS token to the `token` file
3. Run certbot in manual mode

#### Usage:
Getting a certificate (or several) :
```sh
# create and change permissions to needed directories
sudo mkdir -p /etc/letsencrypt
sudo chown your-user: /etc/letsencrypt

sudo mkdir -p /var/log/letsencrypt
sudo chown your-user: /var/log/letsencrypt
```

```sh
# run certbot to obtain the certificate for your fqdn
certbot certonly --manual --preferred-challenges dns \
  [--non-interactive] [--quiet] [--agree-tos] [--manual-public-ip-logging-ok] \
  --manual-auth-hook $(pwd)/challenge-hook.sh \
  --manual-cleanup-hook $(pwd)/cleanup-hook.sh \
  --email your.email@here.net \
  [--domain yourdomain.duckdns.org \]
  --domain *.yourdomain.duckdns.org \
  --logs-dir /var/log/letsencrypt
```

Example renew cron job:

```
* * * * 1 /path/to/certbot renew
```
