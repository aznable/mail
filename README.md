# Aznable Mail

An implementation of [Docker Mailserver](https://github.com/docker-mailserver/docker-mailserver) and [Rainloop](https://github.com/hardware/rainloop)

## Installation

Install `Aznable Mail` by cloning its Github repository:

```
git clone https://github.com/aznable/mail.git
cd mail
cp .env.example .env
chmod a+x mail.sh
```

## Initial Configuration

Replace `HOSTNAME` and `DOMAIN` from the `.env` file with the server hostname and its registered domain name:

```
###################################
# Mailserver settings
###################################
HOSTNAME=aznable
DOMAIN=aznable.test
ONE_DIR=0
POSTMASTER_ADDRESS=me@aznable.test
TIMEZONE=Asia/Manila
```

For the Rainloop webmail, the configuration is already set for a reverse proxy (using [Aznable Infra](https://github.com/aznable/infra)):

```
###################################
# Let's Encrypt settings
###################################
LETSENCRYPT_EMAIL=me@aznable.test
LETSENCRYPT_HOST=mail.aznable.test

###################################
# NGINX Proxy settings
###################################
VIRTUAL_HOST=mail.aznable.test
VIRTUAL_PATH=/
VIRTUAL_PORT=8888
```

However, if the implementation doesn't need a reverse proxy, kindly check the tutorial in this [link](https://jzweig.com/blog/setup-your-own-email-server-with-docker/) for the setup.

## Basic Usage

To run the containers, just execute `docker-compose up -d` in the same directory:

```
$ docker-compose up -d
```

Once the mail server has started, create its first user:

```
$ mail.sh email add [EMAIL] [PASSWORD]
```

Then execute the generation of DKIM keys:

```
$ mail.sh config dkim
```