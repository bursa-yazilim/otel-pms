# Local Development Environment — M0 Baseline

## Status

**SELECTED BASELINE / RUNTIME VALIDATION PENDING**

This document defines the standard Bursa Yazılım local development environment for Otel PMS before the first clean-install smoke test.

The purpose is to avoid developing against an accidental machine configuration that cannot be reproduced on customer/shared-hosting environments later.

## Selected Bursa Yazılım baseline

Primary local development target:

- OS: Windows 11
- Web stack: WAMP / Apache
- PHP: **8.3.x, 64-bit Thread Safe for Apache/WAMP**
- Database: **MySQL 8.x**
- Composer: current Composer 2.x compatible with PHP 8.3
- Browser: current Chromium-based browser for installer/front/back-office smoke tests
- Time zone for Turkey test environment: `Europe/Istanbul`
- Character set expectation: UTF-8 / utf8mb4 where supported by current schema/runtime

This is the Bursa development baseline, not yet the final minimum production requirement. Production compatibility will be documented after clean-install and hosting tests.

## Upstream requirements observed at baseline commit

Current QloApps `develop` metadata at baseline commit `7318ae2c0056e1e0d4167424c942a28053ad1b08` states:

- README: PHP 8.1–8.4
- README: MySQL 5.7–8.4
- `composer.json`: PHP `>8.0 <8.5`

Current `composer.json` requires:

- `ext-curl`
- `ext-dom`
- `ext-gd`
- `ext-mcrypt`
- `ext-openssl`
- `ext-pdo_mysql`
- `ext-phar`
- `ext-simplexml`
- `ext-soap`
- `ext-zip`

Do not remove or loosen these Composer requirements during M0 merely to make an installation pass. First determine whether the requirement is actually used and whether the clean environment can satisfy it.

## mcrypt finding

`ext-mcrypt` requires explicit attention.

Facts recorded for M0:

- mcrypt was removed from the PHP core as of PHP 7.2.
- it remains available as an external PECL extension.
- PECL mcrypt 1.0.9 provides PHP 8.3 Windows builds, including Thread Safe x64 suitable for a typical 64-bit Apache/WAMP PHP 8.3 setup.
- the PECL package itself describes libmcrypt/mcrypt as unmaintained.

M0 decision:

1. **Do not remove `ext-mcrypt` from `composer.json` yet.**
2. Attempt the baseline clean install with the extension present.
3. Record whether QloApps runtime actually calls mcrypt functionality in our tested workflows.
4. If the extension becomes a deployment burden, create a separate technical decision before changing upstream requirements or replacing crypto usage.
5. Never replace cryptographic behavior casually; any migration must account for existing encrypted data compatibility.

## Pre-install checks — Windows/WAMP

Run these from a terminal that uses the same PHP executable/version as Apache/WAMP.

```powershell
php -v
php --ini
php -m
composer --version
composer check-platform-reqs
```

Confirm at minimum that the PHP module list contains equivalents of:

```text
curl
dom
gd
mcrypt
openssl
PDO
pdo_mysql
Phar
SimpleXML
soap
zip
```

Also verify:

```powershell
php -r "echo PHP_VERSION, PHP_EOL;"
php -r "echo PHP_INT_SIZE === 8 ? '64-bit' : '32-bit', PHP_EOL;"
php -r "echo date_default_timezone_get(), PHP_EOL;"
php -r "var_export(extension_loaded('mcrypt')); echo PHP_EOL;"
php -r "var_export(extension_loaded('pdo_mysql')); echo PHP_EOL;"
```

## WAMP/Apache requirements to verify

Before marking runtime baseline validated:

- Apache starts cleanly with selected PHP 8.3 version.
- `mod_rewrite` is enabled if the application/runtime requires rewritten URLs.
- `.htaccess` overrides are allowed for the project directory where needed.
- PHP `memory_limit` is at least 128M for the upstream-recommended baseline.
- `upload_max_filesize` is at least 16M for the upstream-recommended baseline.
- `max_execution_time` is at least 500 during installer validation unless a better tested value is established later.
- `allow_url_fopen` behavior is recorded.
- HTTPS is not required for localhost smoke testing, but is mandatory for production handling of credentials and sensitive guest data.

## Database baseline

Initial local clean-install target:

```text
Database server: MySQL 8.x
Database name: otel_pms
Character encoding: use installer/current QloApps defaults first; record actual schema/collation after install
```

M0 rule:

- Use an empty database for the clean-install baseline.
- Do not import the old QloApps 1.7.0 ZIP database or fixtures as a substitute for the current `develop` installer.
- Do not manually patch schema errors before recording the original installer failure.

## Mail baseline

Email delivery is not a prerequisite for the first installer pass, but before M0 closes we must determine:

- whether local mail can be disabled/safely mocked for smoke tests,
- how SMTP is configured,
- whether failed mail delivery can break reservation/payment workflows,
- which transactional email events matter for the Turkey Edition.

Production SMTP credentials must never be committed to Git.

## Cron baseline

Before M0 closes:

- validate `qlocrontaskmanager` behavior in a running install,
- identify which QloApps features depend on scheduled execution,
- document Windows-local test method,
- document Linux/cPanel/shared-hosting production cron method,
- ensure Turkey integrations can use scheduled jobs without requiring SSH-only deployment.

## Clean-install target path

Recommended Windows/WAMP project path:

```text
D:\wamp\www\otel-pms
```

Repository source must come from the Bursa GitHub repository/working branch. The separately downloaded `qloapps-1.7.0.zip` is not a source input.

## Clean-install smoke-test sequence

After environment prerequisites pass:

1. create empty `otel_pms` database,
2. open the QloApps installer from the current project source,
3. complete installation without modifying source files,
4. record installer warnings/errors,
5. log in to back office,
6. load front office,
7. configure one test property,
8. create one room type and at least three rooms,
9. create a direct reservation,
10. confirm reservation in back office,
11. test baseline check-in,
12. test baseline check-out,
13. observe payment-status/basic payment behavior,
14. observe cancellation behavior,
15. record application/PHP/Apache/MySQL errors.

## M0 exit evidence required from runtime

This document may change from **RUNTIME VALIDATION PENDING** to validated only after we have recorded actual outputs for:

- PHP version,
- PHP loaded configuration path,
- required extensions,
- MySQL version,
- Composer platform check,
- installer result,
- admin login,
- front office,
- booking,
- check-in,
- check-out,
- payment baseline,
- cancellation baseline.

No runtime test is considered passed merely because upstream documentation says the version is supported.