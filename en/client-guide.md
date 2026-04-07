# ACME Certificate Renewal Guide (Certbot, acme.sh)
**Management > Private CA > ACME Certificate Renewal Guide (Certbot, acme.sh)**

The Private CA service supports the ACME (Automatic Certificate Management Environment) protocol, enabling automatic certificate issuance and renewal. By using an ACME client (e.g., Certbot, acme.sh), you can issue and periodically renew certificates without manual intervention.

This guide describes how to issue and automatically renew certificates using Certbot or acme.sh with the Private CA ACME server.

!!! tip "Note"
    - **ACME (Automatic Certificate Management Environment)**: A standard protocol that automates certificate issuance and renewal.
    - **Certbot**: An ACME client tool developed by Let's Encrypt that automatically issues and renews certificates.
    - **acme.sh**: A lightweight ACME client written in pure Unix Shell that automatically issues and renews certificates.
    - **Base certificate**: A certificate that serves as a template referenced during ACME automatic renewal.
    - **CSR (Certificate Signing Request)**: A signing request file used to request certificate issuance.
    - **EAB (External Account Binding)**: Account binding information used to authenticate with the ACME server.

## Prerequisites

Before starting certificate issuance through ACME, you need to prepare the following.

### 1. Issue a Base Certificate

The base certificate serves as a "template" that the ACME server references during automatic renewal.

- Only certificates with the same domains (CN, SAN) as those configured in the base certificate can be renewed through ACME.
- The base certificate is created through the standard certificate issuance procedure in the console.
- After issuing the base certificate, use the certificate ID in the ACME Directory URL.

### 2. Check ACME Server Information

Check the following information in the Private CA console.

- **ACME Directory URL**: `https://kr1-pca.api.nhncloudservice.com/acme/v2.0/cert/{certId}/directory`
- **ACME Token ID**: The ACME token ID issued from the console (**YOUR_ACME_TOKEN_ID**)
- **ACME HMAC Key**: The ACME token HMAC key issued from the console (**YOUR_ACME_TOKEN_HMAC_KEY**)

## Renewing Certificates

You can use Certbot or acme.sh as your ACME client. Choose the tool that suits your environment.

- **Certbot**: A widely used ACME client developed by Let's Encrypt, based on Python.
- **acme.sh**: A lightweight ACME client written in pure Shell script, with minimal dependencies and simple installation.

!!! tip "Note"
    To automatically manage certificates in a Kubernetes environment, see [ACME Certificate Renewal Guide (cert-manager)](cert-manager-guide.md).

### Certificate Renewal with Certbot

#### Install Certbot

Certbot is the most widely used ACME client. Refer to the [official Certbot documentation](https://certbot.eff.org/) to install it for your operating system.

**Installation example (Ubuntu/Debian)**

```bash
sudo apt update
sudo apt install certbot
```

**Installation example (CentOS/RHEL)**

```bash
sudo yum install certbot
```

#### Command Configuration

The following is an example of a basic certificate issuance command.

```bash
certbot certonly \
  --manual \
  --manual-auth-hook ./pre.sh \
  --deploy-hook ./post.sh \
  --preferred-challenges http \
  --server https://kr1-pca.api.nhncloudservice.com/acme/v2.0/cert/{certId}/directory \
  -d example.com -d www.example.com \
  --eab-kid "YOUR_ACME_TOKEN_ID" \
  --eab-hmac-key "YOUR_ACME_TOKEN_HMAC_KEY" \
  --key-type rsa \
  --rsa-key-size 2048 \
  --agree-tos \
  --register-unsafely-without-email
```

#### Key Options

| Option | Description | Required | Default |
|------|------|------|--------|
| `--manual` | Performs challenge verification manually. Uses manual mode instead of automatic Apache or Nginx configuration. | O | - |
| `--manual-auth-hook` | Specifies a script to run before challenge verification. Even an empty script is required to prevent errors during renewal. | O | - |
| `--deploy-hook` | Specifies a script to run after successful certificate issuance. Used for post-processing such as moving or deploying certificates. | X | - |
| `--preferred-challenges` | Specifies the challenge method (`http`, `dns`, `tls-alpn`). Generally, `http` is used. | O | - |
| `--server` | Specifies the ACME server's Directory URL. | O | - |
| `-d` | Specifies the domains to include in the certificate. You must check the CN and SAN of the base certificate in the console and enter them exactly. | O | - |
| `--eab-kid` | The key ID for External Account Binding. Enter the ACME token ID issued from Private CA. | O | - |
| `--eab-hmac-key` | The EAB HMAC key (Base64-encoded). Enter the ACME token HMAC key issued from Private CA. | O | - |
| `--key-type` | Specifies the private key type (`rsa`, `ecdsa`). | X | rsa |
| `--rsa-key-size` | Specifies the RSA key length. Used only when `--key-type rsa`, with values of `2048`, `3072`, or `4096`. | X | 2048 |
| `--elliptic-curve` | Specifies the ECDSA key curve. Used only when `--key-type ecdsa`, with values of `secp256r1`, `secp384r1`, or `secp521r1`. | X | secp256r1 |
| `--agree-tos` | Automatically agrees to the terms of service. Prevents interactive input. | X | - |
| `--register-unsafely-without-email` | Registers an account without an email. Prevents interactive input. | X | - |

!!! tip "Note"
    - `--manual` mode is used for manual challenge verification.
    - `manual-auth-hook` is required to ensure stability during certificate renewal.
    - Using `deploy-hook`, you can automatically perform deployment and post-processing tasks after certificate issuance.
    - `--server`, `--eab-kid`, and `--eab-hmac-key` are required for integration with the Private CA ACME server.

!!! danger "Caution"
    When specifying domains, you must enter the CN (Common Name) and domain SAN (Subject Alternative Name) configured in the base certificate exactly. Before issuing the certificate, check the CN and SAN information of the base certificate in the console and verify that the correct domains are specified in the `-d` option.

#### Hook Script Examples

##### pre.sh (Pre-authentication Script)

The `manual-auth-hook` must exist as a file even if the content is empty. This is to prevent errors during certificate renewal.

```bash
#!/bin/bash
# You can add any required pre-authentication tasks here.
```

##### post.sh (Post-issuance Script)

The `deploy-hook` is executed only when the certificate is successfully issued.

```bash
#!/bin/bash
# Post-processing tasks after certificate issuance
echo "[post.sh] Certificate issuance complete!"

# Copy certificates to the desired location
cp /etc/letsencrypt/live/example.com/fullchain.pem ~/Downloads/
cp /etc/letsencrypt/live/example.com/privkey.pem ~/Downloads/

# Additional tasks such as restarting the web server
# systemctl reload nginx
```

#### Verify Issued Certificate

By default, certificates are stored in the following path.

```
/etc/letsencrypt/live/<domain name (CN)>/
├── cert.pem          # Server certificate
├── chain.pem         # Intermediate certificate chain
├── fullchain.pem     # cert.pem + chain.pem
└── privkey.pem       # Private key
```

##### Check Certificate Details

```bash
# Check certificate information
openssl x509 -in /etc/letsencrypt/live/<domain name (CN)>/cert.pem -text -noout

# Check certificate validity period
openssl x509 -in /etc/letsencrypt/live/<domain name (CN)>/cert.pem -noout -dates
```

#### Configure Automatic Certificate Renewal

Certbot can automatically renew certificates that are about to expire.

##### Renewal Prerequisites

- There must be a prior issuance history.
- The `/etc/letsencrypt/renewal/<domain>.conf` file must exist.
- Certificate files must exist in the `/etc/letsencrypt/live/<domain>/` directory.

##### Automatic Renewal Settings

When Certbot is installed, a cron job or systemd timer is automatically registered to periodically check certificate expiration.

**Default renewal cycle**: Automatic renewal attempts begin 30 days before expiration

##### Manual Renewal

You can perform manual renewal with the following commands as needed.

```bash
# Attempt to renew all certificates
sudo certbot renew

# Force renewal
sudo certbot renew --force-renewal
```

##### Register Cron Job

If automatic renewal is not registered, you can manually add a cron job.

```bash
# Edit crontab
sudo crontab -e

# Check for renewal at 2 AM daily
0 2 * * * certbot renew --no-random-sleep-on-renew
```

##### Change Renewal Cycle

You can adjust the renewal cycle in the `/etc/letsencrypt/renewal/<domain>.conf` file.

```ini
[renewalparams]
renew_before_expiry = 30 days
```

You can change the `renew_before_expiry` value to configure how many days before expiration the renewal attempt should begin.

!!! danger "Caution"
    - The ED25519 key type is currently not supported by Certbot. Issuance and renewal are not possible if the certificate chain contains a certificate using the ED25519 algorithm.
    - The certificate chain must consist of at least 3 levels (Root → Intermediate → Leaf).
    - The `renew_before_expiry` value should be adjusted carefully, taking into account the ACME server's rate limit policy.
    - The cron job automatically registered during Certbot installation may contain default options, so it is recommended to modify the `/etc/cron.d/certbot` file as needed.
    - The default cron job includes a random delay (`perl -e 'sleep int(rand(43200))'`). This is to prevent overloading the ACME server. If immediate execution is needed, remove that statement or use the `--no-random-sleep-on-renew` option.

#### Troubleshooting

##### When Certificate Issuance Fails

1. **Check the ACME Directory URL**: Verify that the URL in the `--server` option is correct.
2. **Check EAB credentials**: Verify that the `--eab-kid` and `--eab-hmac-key` values are correct.
3. **Domain verification failure**: Verify that the challenge method is appropriate for your environment. For HTTP Challenge, port 80 must be open.
4. **Hook script permissions**: Verify that the `pre.sh` and `post.sh` files have execution permissions.

##### When Certificate Renewal Fails

1. **Check renewal configuration**: Verify that the `/etc/letsencrypt/renewal/<domain>.conf` file exists and is correct.
2. **Check hook script existence**: Verify that the script specified in `manual-auth-hook` still exists.

### Certificate Renewal with acme.sh

acme.sh is a lightweight ACME client written in pure Unix Shell. It has minimal dependencies and simple installation, making it suitable for a wide variety of environments.

#### Install acme.sh

acme.sh can be easily installed using the installation script.

**Installation**

```bash
curl https://get.acme.sh | sh
```

After installation is complete, load the environment variables.

```bash
. ~/.acme.sh/acme.sh.env
acme.sh --version
```

!!! tip "Note"
    - When reconnecting to a container or a new shell session, you must reload the environment variables using the `. ~/.acme.sh/acme.sh.env` command.
    - An email address is optional during installation.

**Installation example (manual download)**

```bash
git clone https://github.com/acmesh-official/acme.sh.git
cd acme.sh
./acme.sh --install
```

#### Register ACME Account

Before issuing a certificate, you must first register an account with the ACME server.

```bash
acme.sh --register-account \
  --server https://kr1-pca.api.nhncloudservice.com/acme/v2.0/cert/{certId}/directory \
  --eab-kid "YOUR_ACME_TOKEN_ID" \
  --eab-hmac-key "YOUR_ACME_TOKEN_HMAC_KEY"
```

!!! danger "Caution"
    - Account registration only needs to be performed **once**.
    - After registration, you can omit the `--eab-kid` and `--eab-hmac-key` options when issuing certificates.

#### Issue Certificate

After account registration, you can issue a certificate.

**Basic issuance command example**

```bash
acme.sh --issue \
  -d example.com -d www.example.com \
  --server https://kr1-pca.api.nhncloudservice.com/acme/v2.0/cert/{certId}/directory \
  --keylength 2048 \
  --standalone
```

#### Key Options

| Option | Description | Required | Default |
|------|------|------|--------|
| `--register-account` | Registers an account with the ACME server. Only needs to be run once. | O (first time) | - |
| `--issue` | Issues a certificate. | O | - |
| `--server` | Specifies the ACME server's Directory URL. | O | - |
| `--eab-kid` | The key ID for External Account Binding. Enter the ACME token ID issued from Private CA. Only required during account registration. | O (registration) | - |
| `--eab-hmac-key` | The EAB HMAC key (Base64-encoded). Enter the ACME token HMAC key issued from Private CA. Only required during account registration. | O (registration) | - |
| `-d` | Specifies the domains to include in the certificate. You must check the CN and SAN of the base certificate in the console and enter them exactly. Multiple domains can be specified. | O | - |
| `--standalone` | Handles HTTP-01 Challenge in standalone mode. acme.sh runs a temporary web server. | O | - |
| `--httpport` | Specifies the port number to use for HTTP-01 Challenge. | X | 80 |
| `--keylength` | Specifies the private key length. For RSA, values of `2048`, `3072`, or `4096` can be used. For ECDSA, values of `ec-256`, `ec-384`, or `ec-521` can be used. | X | 2048 |
| `--debug` | Runs in debug mode and outputs detailed logs. | X | - |

!!! tip "Note"
    - In `--standalone` mode, acme.sh runs a temporary web server to handle the challenge. Port 80 must be available.
    - After account registration, you can issue certificates without the `--eab-kid` and `--eab-hmac-key` options.

!!! danger "Caution"
    When specifying domains, you must enter the CN (Common Name) and domain SAN (Subject Alternative Name) configured in the base certificate exactly. Before issuing the certificate, check the CN and SAN information of the base certificate in the console and verify that the correct domains are specified in the `-d` option.

#### Issue Certificate in Standalone Mode

acme.sh runs a temporary web server to handle HTTP-01 Challenge.

```bash
acme.sh --issue \
  -d example.com \
  --server https://kr1-pca.api.nhncloudservice.com/acme/v2.0/cert/{certId}/directory \
  --keylength 2048 \
  --standalone
```

!!! danger "Caution"
    - Port 80 must be open and available.
    - If an existing web server is using port 80, it must be temporarily stopped.
    - To use a different port, add the `--httpport` option.

#### Verify Issued Certificate

By default, certificates are stored in the following path.

```
~/.acme.sh/<domain name (CN)>/
├── <domain name>.cer        # Server certificate (leaf certificate)
├── <domain name>.key        # Private key
├── ca.cer                   # CA chain (Intermediate + Root)
└── fullchain.cer            # Full chain (leaf certificate + CA chain)
```

!!! tip "Note"
    - `<domain name>.cer`: Contains only the leaf certificate
    - `fullchain.cer`: Full chain including the leaf certificate + intermediate certificate + root certificate
    - `ca.cer`: CA chain (intermediate certificate + root certificate)

##### Check Certificate Details

```bash
# Check certificate information
openssl x509 -in ~/.acme.sh/example.com/example.com.cer -text -noout

# Check certificate validity period
openssl x509 -in ~/.acme.sh/example.com/example.com.cer -noout -dates
```

#### Install (Deploy) Certificate

acme.sh can copy certificates to the desired location and restart the web server using the `--install-cert` command.

**Nginx example**

```bash
acme.sh --install-cert -d example.com \
  --key-file       /etc/nginx/ssl/privkey.pem \
  --cert-file      /etc/nginx/ssl/cert.pem \
  --fullchain-file /etc/nginx/ssl/fullchain.pem \
  --ca-file        /etc/nginx/ssl/ca.pem \
  --reloadcmd      "nginx -s reload"
```

**Apache example**

```bash
acme.sh --install-cert -d example.com \
  --key-file       /etc/apache2/ssl/privkey.pem \
  --cert-file      /etc/apache2/ssl/cert.pem \
  --fullchain-file /etc/apache2/ssl/fullchain.pem \
  --ca-file        /etc/apache2/ssl/ca.pem \
  --reloadcmd      "systemctl reload apache2"
```

!!! tip "Note"
    - `--key-file`: Path to save the private key file
    - `--cert-file`: Path to save the leaf certificate
    - `--fullchain-file`: Path to save the full chain (leaf + CA chain)
    - `--ca-file`: Path to save the CA chain
    - `--reloadcmd`: Command to automatically execute after certificate installation

#### Configure Automatic Certificate Renewal

acme.sh automatically registers a cron job during installation to check for certificate expiration and perform renewal.

##### Renewal Prerequisites

- There must be a prior issuance history.
- Certificate files must exist in the `~/.acme.sh/<domain>/` directory.

##### Automatic Renewal Settings

A cron job is automatically registered when acme.sh is installed.

**Default renewal cycle**: Automatic renewal attempts begin 60 days before expiration

**Check Cron Job**

```bash
crontab -l | grep acme.sh
```

It is typically registered in the following format.

```
0 0 * * * "/home/user/.acme.sh"/acme.sh --cron --home "/home/user/.acme.sh" > /dev/null
```

##### Manual Renewal

You can perform manual renewal with the following commands as needed.

```bash
# Attempt to renew all certificates
acme.sh --cron

# Force renewal of a specific certificate
acme.sh --renew -d example.com --force
```

##### Change Renewal Cycle

By default, acme.sh attempts renewal 60 days before expiration. To change this value, modify the `~/.acme.sh/account.conf` file.

```bash
# Edit account.conf
vim ~/.acme.sh/account.conf
```

Add or modify the following line.

```
Le_RenewalDays=30
```

With this configuration, renewal attempts will begin 30 days before expiration.

!!! danger "Caution"
    - The ED25519 key type may not currently be supported by acme.sh. Issuance and renewal are not possible if the certificate chain contains a certificate using the ED25519 algorithm.
    - The certificate chain must consist of at least 3 levels (Root → Intermediate → Leaf).
    - The `Le_RenewalDays` value should be adjusted carefully, taking into account the ACME server's rate limit policy.
    - When using standalone mode, port 80 must be available during renewal, so a script to temporarily stop the web server may be required.

#### Troubleshooting

##### When Certificate Issuance Fails

1. **Check the ACME Directory URL**: Verify that the URL in the `--server` option is correct.
2. **Check EAB credentials**: Verify that account registration has been completed. If not, register the account first using the `--register-account` command.
3. **Domain verification failure**: Verify that port 80 is open and available. If an existing web server is using port 80, it must be temporarily stopped.
4. **Debug mode**: Add the `--debug` option to check detailed logs.

```bash
acme.sh --issue \
  -d example.com \
  --server https://kr1-pca.api.nhncloudservice.com/acme/v2.0/cert/{certId}/directory \
  --keylength 2048 \
  --standalone \
  --debug
```

##### When Certificate Renewal Fails

1. **Check certificate information**: Verify that the settings used during the initial issuance are still intact.
2. **Check cron job**: Verify that the cron job is properly registered.
3. **Check logs**: Check for error messages in the `~/.acme.sh/<domain>/<domain>.log` file.
4. **Manual renewal test**: Attempt manual renewal with the `acme.sh --renew -d example.com --force --debug` command to diagnose the issue.

## ACME Protocol Information

Through the ACME Directory URL (`/directory`) provided by Private CA, ACME clients automatically retrieve all necessary endpoint information.

The entire ACME protocol flow is handled automatically by the client, so users only need to provide the Directory URL.

For more details on the ACME protocol, see [RFC 8555](https://datatracker.ietf.org/doc/html/rfc8555).

## References

- [Official Certbot documentation](https://certbot.eff.org/)
- [Official acme.sh documentation](https://github.com/acmesh-official/acme.sh)
- [acme.sh DNS API list](https://github.com/acmesh-official/acme.sh/wiki/dnsapi)
- [ACME Protocol Specification (RFC 8555)](https://datatracker.ietf.org/doc/html/rfc8555)
- [Let's Encrypt - Challenge Types](https://letsencrypt.org/docs/challenge-types/)
- [ACME Certificate Renewal Guide (cert-manager)](cert-manager-guide.md)