# M0 Checklist — Foundation, Upstream and Commercial Viability

## Status

**IN PROGRESS**

M0 establishes a trustworthy baseline before Turkey Edition feature development begins.

## Repository baseline

- [x] Confirm upstream repository: `Qloapps/QloApps`
- [x] Confirm product repository: `bursa-yazilim/otel-pms`
- [x] Confirm fork `develop` baseline commit: `7318ae2c0056e1e0d4167424c942a28053ad1b08`
- [x] Exclude downloaded QloApps 1.7.0 ZIP from project source-of-truth workflow
- [x] Reserve `develop` for upstream tracking
- [x] Create `main` product branch
- [x] Create M0 working branch `chore/m0-foundation`

## Documentation foundation

- [x] `docs/ARCHITECTURE.md`
- [x] `docs/QLOAPPS_UPSTREAM.md`
- [x] `docs/LICENSING.md`
- [x] `docs/MODULE_LICENSE_INVENTORY.md`
- [x] `docs/EXTENSION_POINTS.md`
- [x] `docs/TURKEY_REQUIREMENTS.md`
- [x] `docs/ROADMAP.md`
- [x] `docs/AI_HANDOFF.md`
- [x] `docs/M0_CHECKLIST.md`

## License / commercial gate

- [x] Confirm root package declares OSL-3.0
- [x] Confirm upstream README explicitly says Webkul-authored modules use their module-root `LICENSE.md`
- [x] Identify separate restrictive module license at `modules/hotelreservationsystem/LICENSE.md`
- [x] Identify additional conflicting/restrictive examples (`qlochannelmanagerconnector`, `qlohotelreview`, `qlopaypalcommerce`, `wkhotelroom`, `wkabouthotelblock`)
- [x] Create first-pass module license inventory
- [ ] Complete exhaustive license inventory for all modules/themes/bundled third-party components
- [ ] Clarify conflicting commercial redistribution/derivative rights for `hotelreservationsystem`
- [ ] Clarify whether other conflicting Webkul module headers or module-root license files control distribution
- [ ] Record paid addon/service licensing model separately
- [ ] Validate intended Bursa Yazılım resale/installation/license model before commercial release

### Current blocker

The source now contains a material license contradiction: several module PHP headers say OSL-3.0 while their module-root `LICENSE.md` contains a restrictive Webkul Software Licence Agreement. The QloApps README explicitly directs Webkul-authored modules to their root `LICENSE.md`, so this cannot safely be ignored. Until written clarification or an approved replacement strategy exists, commercial release remains BLOCKED while technical M0 work continues.

## Runtime baseline

Known from current `develop` README/composer metadata:

- PHP: current README supports PHP 8.1–8.4; composer constraint is `>8.0 <8.5`
- MySQL: current README states 5.7–8.4
- curl
- dom
- gd
- mcrypt (composer currently declares it; runtime availability must be verified)
- openssl
- PDO MySQL
- phar
- simplexml
- soap
- zip

Still required:

- [ ] Select/record standard Bursa Yazılım local development PHP version
- [ ] Select/record supported MySQL/MariaDB baseline
- [ ] Verify required PHP extensions in a clean environment
- [ ] Reconcile composer `ext-mcrypt` declaration with supported modern PHP runtime/install behavior
- [ ] Record web server/rewrite requirements
- [ ] Record cron requirements
- [ ] Record mail requirements

## Clean-install baseline

- [ ] Fresh database created
- [ ] QloApps installer completes without manual source patching
- [ ] Admin login works
- [ ] Front-office site loads
- [ ] Test property/hotel can be configured
- [ ] Room type/room can be created
- [ ] Direct reservation can be created
- [ ] Reservation appears correctly in back office
- [ ] Check-in baseline validated
- [ ] Check-out baseline validated
- [ ] Payment status/basic payment flow observed
- [ ] Cancellation baseline observed
- [ ] Relevant logs/errors recorded

## Architecture validation

### Source review completed

- [x] Confirm module pattern (`Module` / `PaymentModule`, install, config, controllers, hooks)
- [x] Identify existing hotel webservice resources
- [x] Identify likely Turkey guest identity extension area
- [x] Identify likely KBS integration boundary
- [x] Identify payment-provider extension pattern from existing payment module
- [x] Identify SMS notification module strategy
- [x] Document initial extension map in `docs/EXTENSION_POINTS.md`

### Runtime validation pending

- [ ] Confirm actual hook/event execution for Turkey Edition features
- [ ] Confirm reliable check-in/check-out lifecycle event or identify need for minimal new hook
- [ ] Confirm cancellation/refund lifecycle hooks
- [ ] Confirm override conventions, precedence and cache behavior
- [ ] Confirm theme/template customization path in running install
- [ ] Confirm Guest Registration Card persistence versus generated display data
- [ ] Confirm cron/task manager behavior
- [ ] Confirm API/webservice authentication and permissions
- [ ] Create `docs/CORE_PATCHES.md` if any unavoidable core change is identified

## Security / data baseline

- [ ] Identify where all guest identity data is persisted
- [ ] Identify authentication/session model
- [ ] Identify audit/logging capabilities
- [ ] Review file upload surfaces relevant to product use
- [ ] Review secrets/config storage method
- [ ] Record backup/restore baseline

## M0 closure rule

M0 may be marked **CLOSED** only when:

1. technical clean-install and core PMS smoke tests pass,
2. extension points are runtime-validated well enough to begin M1 without blind core edits,
3. license inventory is materially complete,
4. the `hotelreservationsystem` commercial-license blocker is resolved or an approved replacement strategy is documented,
5. `docs/AI_HANDOFF.md` contains the exact next step for M1.

Until then, status remains **IN PROGRESS**.
