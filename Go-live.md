This page documents necessary steps required in order to go live, including production environment setup and configurations needed from the client however still not obtained or too sensitive to persist in codebase.

# Functional setup (Involve: Client)

## Initialise default package

[GETMARRIED-136](https://ampersand.atlassian.net/browse/GETMARRIED-136)

## Set up Stripe integration

### Webhooks

Set up Stripe production account with the webhooks and whitelist Stripe webhook IPs

Stripe IPs: https://stripe.com/docs/ips#webhook-ip-addresses

URL: `https://gettingmarried.co.uk/api/stripe/webhooks` (without tailing slash)

Event types:
- invoice.created
- invoice.payment_succeeded

Note: incorrect webhook setup will result in subscription failed to renew or cancel after payment success or failure (See: GETMARRIED-328).

Package is made default by UserAdmin and the system do not initialise this data. Before we go live, during UAT / Soft Launch phase, we are expected to make sure a default package is in place.

# Environment (Involve: DevOps / SystemAdmin)

## Environment variables

Review `.env.dist` file and set up environment variables referencing to it.

**IMPORTANT: Don't source from .env / .env.dist files as they are committed to codebase for test environments' use only and not safe for production** 

See: https://12factor.net/config

## JWT public / private keys

We use [JWT Bundle](https://github.com/lexik/LexikJWTAuthenticationBundle/blob/master/Resources/doc/index.md#installation) to manage API (e.g., REST) access.

Generate the SSH keys :

```bash
$ mkdir -p config/jwt
$ openssl genrsa -out config/jwt/private.pem -aes256 4096
$ openssl rsa -pubout -in config/jwt/private.pem -out config/jwt/public.pem
```

In case first openssl command forces you to input password use following to get the private key decrypted:

```bash
$ openssl rsa -in config/jwt/private.pem -out config/jwt/private2.pem
$ mv config/jwt/private.pem config/jwt/private.pem-back
$ mv config/jwt/private2.pem config/jwt/private.pem
```

Add environment variables:

```
JWT_SECRET_KEY=%kernel.project_dir%/config/jwt/private.pem
JWT_PUBLIC_KEY=%kernel.project_dir%/config/jwt/public.pem
JWT_PASSPHRASE=99f9afbea033ea556401591b7593bbd2
```

**NOTE 1:** we use an alternative dir `systems/jwt/` for test environments so that we can commit the keys for sharing. We intend to live `config/jwt/` dir empty and only for production use.

**NOTE 2:** make sure to generate a new `JWT_PASSPHRASE` key for production