[![Release](https://img.shields.io/github/v/release/bloodhunterd/froxlor-mail-docker?include_prereleases&style=for-the-badge)](https://github.com/bloodhunterd/froxlor-mail-docker/releases)
[![Docker Build](https://img.shields.io/docker/cloud/build/bloodhunterd/froxlor-mail?style=for-the-badge)](https://hub.docker.com/r/bloodhunterd/froxlor-mail)
[![License](https://img.shields.io/github/license/bloodhunterd/froxlor-mail-docker?style=for-the-badge)](https://github.com/bloodhunterd/froxlor-mail-docker/blob/master/LICENSE)

# Froxlor Mail

Docker Image of Froxlor Mail Server.

## Configuration

### Environment

| ENV | Values¹ | Default | Description
|--- |--- |--- |---
| FRX_MAIL_DIR | Absolute path | /var/customers/mail | Path to the Froxlor customer mails.
| FRX_DB_HOST | Hostname / IP | localhost | Froxlor database hostname or IP
| FRX_DB_NAME | Database name | froxlor | Froxlor database name
| FRX_DB_USER | Database user | froxlor | Froxlor database user
| FRX_DB_PASSWORD | Database user password |  | Froxlor database user password
| ROOT_ALIAS | Email address | root@example.com | Email address alias for internal mails to the root user.
| MAIL_DOMAIN | Domain | example.com | Mail domain
| POSTMASTER_ADDRESS | Email address | postmaster@example.com | Postmaster email address
| CLEANUP_TRASH | 0 - ... | 30 | Time in days after mails in Trash folder will be deleted.
| CLEANUP_SPAM | 0 - ... | 60 | Time in days after mails in Spam folder will be deleted.

¹ *Possible values are separated by a slash or a range is indicated by a dash.*

### Volumes

```bash
volumes:
  - ./mail/:/var/customers/mail/
```

### Scheduled tasks

Add the following lines to the host [crontab](https://www.linuxwiki.de/crontab), to cleanup Trash and Spam folders automatically.

```bash
# Cleanup Spam
0 4 * * * /usr/bin/docker exec froxlor-mail /bin/bash -c '/srv/cleanup-spam.sh'
# Cleanup Trash
0 4 * * * /usr/bin/docker exec froxlor-mail /bin/bash -c '/srv/cleanup-trash.sh'
```

## Update

Please note the [changelog](https://github.com/bloodhunterd/froxlor-mail-docker/blob/master/CHANGELOG.md) to check for configuration changes before updating.

## Build With

* [Postfix](http://www.postfix.org/)
* [Dovecot](https://www.dovecot.org/)
* [Debian](https://www.debian.org/)
* [Docker](https://www.docker.com/)

## Authors

* [BloodhunterD](https://github.com/bloodhunterd)

## License

This project is licensed under the Unlicense - see [LICENSE.md](https://github.com/bloodhunterd/froxlor-mail-docker/blob/master/LICENSE) file for details.
