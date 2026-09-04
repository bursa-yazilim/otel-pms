# M0 Runtime Test Results

## Status

**NOT STARTED — TEMPLATE READY**

This file is the evidence log for the first clean installation and core PMS smoke test of the Bursa Yazılım Otel PMS baseline.

Do not mark any item as passed from documentation assumptions. Record actual command output or observed UI behavior.

## Test identity

- Repository: `bursa-yazilim/otel-pms`
- Branch/commit tested: `TBD`
- Test date: `TBD`
- Tester: `TBD`
- Machine: Windows 11 / WAMP baseline

## 1. Runtime / platform evidence

### PHP

```text
php -v
TBD
```

### Loaded PHP configuration

```text
php --ini
TBD
```

### PHP architecture

```text
php -r "echo PHP_INT_SIZE === 8 ? '64-bit' : '32-bit', PHP_EOL;"
TBD
```

### Required extensions

Record PASS/FAIL for each:

| Extension | Result | Notes |
| --- | --- | --- |
| curl | TBD | |
| dom | TBD | |
| gd | TBD | |
| mcrypt | TBD | |
| openssl | TBD | |
| pdo_mysql | TBD | |
| Phar | TBD | |
| SimpleXML | TBD | |
| soap | TBD | |
| zip | TBD | |

### Composer

```text
composer --version
TBD

composer check-platform-reqs
TBD
```

### MySQL

```text
SELECT VERSION();
TBD
```

### Apache/WAMP

- Apache starts with selected PHP 8.3: TBD
- `mod_rewrite`: TBD
- `.htaccess` overrides: TBD
- local project URL: TBD

## 2. Installer

- Empty database created: TBD
- Database name: `otel_pms`
- Installer launches: TBD
- Requirement screen passes: TBD
- Database connection passes: TBD
- Schema/data installation passes: TBD
- Admin account creation passes: TBD
- Installer completes without source patch: TBD

### Installer warnings/errors

```text
TBD
```

### Manual source patches required

Expected for a clean baseline: **NONE**

```text
TBD
```

If a patch is required, M0 must first record the original failure, affected file, exact reason and whether it is an upstream bug/environment issue.

## 3. Back office / front office smoke tests

| Test | Result | Notes |
| --- | --- | --- |
| Back-office login | TBD | |
| Dashboard loads | TBD | |
| Front-office homepage loads | TBD | |
| No fatal PHP errors | TBD | |
| No material browser-console errors | TBD | |

## 4. Test property setup

Use synthetic demo data only.

Suggested property:

```text
Kapıdağ Boutique Hotel
```

Record:

- Property/hotel created/configured: TBD
- Room type created: `Standart Oda` — TBD
- Physical rooms created: `101`, `102`, `103` — TBD
- Base room price configured: TBD
- Availability displayed correctly: TBD

## 5. Direct reservation baseline

Use synthetic guest data; do not use real TCKN/passport information.

Suggested scenario:

```text
Guest: Ahmet Test
Room: 101 / Standart Oda
Stay: future two-night test range
Source: direct/manual reservation
```

Record:

- Reservation can be created: TBD
- Correct dates/room/price shown: TBD
- Reservation appears in back office: TBD
- Availability decreases correctly: TBD
- Reservation holder data persists: TBD
- Additional staying guests model observed: TBD

## 6. Check-in baseline

- Check-in action exists: TBD
- Check-in succeeds: TBD
- Reservation/room status changes correctly: TBD
- Actual lifecycle hook/event observed: TBD
- Guest-registration behavior observed: TBD
- Relevant database records identified: TBD

### Hook/event notes

```text
TBD
```

This evidence will inform the Turkey KBS integration boundary.

## 7. Check-out baseline

- Check-out action exists: TBD
- Check-out succeeds: TBD
- Room/reservation status changes correctly: TBD
- Actual lifecycle hook/event observed: TBD
- Outstanding balance behavior observed: TBD

### Hook/event notes

```text
TBD
```

## 8. Payment baseline

This test does not require a real card/payment provider.

Observe existing QloApps behavior for:

- unpaid reservation: TBD
- partial/advance payment capability: TBD
- full payment: TBD
- payment record/history: TBD
- refund/cancellation relationship: TBD

No production payment credentials are permitted in M0 test evidence.

## 9. Cancellation baseline

- Reservation cancellation available: TBD
- Availability returns correctly: TBD
- Payment/refund behavior observed: TBD
- Cancellation lifecycle hook/event observed: TBD
- Email/notification side effects observed: TBD

## 10. Module runtime checks relevant to licensing

### `hotelreservationsystem`

- Required for core booking operations: expected YES; runtime confirmation TBD
- Behavior when disabled/unavailable: do not test destructively on the only test database; use disposable installation if needed

### `wkhotelroom`

Static M0 review classifies this as a homepage/front-office presentation module rather than core PMS logic.

Runtime validation:

- disable module on disposable/clean test state: TBD
- booking still functions: TBD
- admin room management still functions: TBD
- only homepage room display affected: TBD

### `wkabouthotelblock`

- disable test: TBD
- expected impact limited to presentation/about content: TBD

### `qlocrontaskmanager`

- module installs/enables: TBD
- scheduled-task behavior: TBD
- shared-hosting compatible trigger method: TBD

## 11. mcrypt runtime observation

- Extension loaded: TBD
- Installer requires it: TBD
- M0 workflows trigger mcrypt-related calls/errors: TBD
- Removing/disabling extension tested on disposable environment only: TBD
- Long-term deployment concern identified: TBD

Do not modify Composer requirements until this evidence is collected and a separate architecture decision is made.

## 12. Logs and errors

Record relevant entries from:

- PHP error log
- Apache error log
- QloApps/application logs if available
- browser console
- MySQL errors

```text
TBD
```

## 13. Security/data observations

During smoke testing identify:

- guest identity tables/fields: TBD
- employee/admin authentication/session storage: TBD
- audit/logging capability: TBD
- uploaded-file locations relevant to PMS: TBD
- secrets/config storage: TBD
- backup/restore mechanism: TBD

## 14. M0 runtime verdict

- Clean install: TBD
- Core reservation: TBD
- Check-in: TBD
- Check-out: TBD
- Payment baseline: TBD
- Cancellation baseline: TBD
- Extension points sufficiently understood for M1: TBD

### Blocking technical issues

```text
TBD
```

### Non-blocking issues / later work

```text
TBD
```

## Completion rule

Only change this document status to **PASSED** after the clean installer and required core PMS flows have actually been tested on the selected baseline environment and material failures have either been fixed/documented or explicitly accepted.
