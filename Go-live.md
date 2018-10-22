This page documents necessary steps required in order to go live, including production environment setup and configurations needed from the client however still not obtained or too sensitive to persist in codebase.

# Environment

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