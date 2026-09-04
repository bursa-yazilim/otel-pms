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
- [x] `docs/TURKEY_REQUIREMENTS.md`
- [x] `docs/ROADMAP.md`
- [x] `docs/AI_HANDOFF.md`
- [x] `docs/M0_CHECKLIST.md`

## License / commercial gate

- [x] Confirm root package declares OSL-3.0
- [x] Identify first separate restrictive module license: `modules/hotelreservationsystem/LICENSE.md`
- [ ] Inventory licenses for all modules/components shipped in the current repository
- [ ] Identify additional separate/commercial/proprietary licenses
- [ ] Clarify commercial redistribution/derivative rights for `hotelreservationsystem`
- [ ] Record paid addon/service licensing model separately
- [ ] Validate intended Bursa Yazılım resale/installation/license model before commercial release

### Current blocker

`modules/hotelreservationsystem/LICENSE.md` contains restrictions that appear incompatible with simply assuming unrestricted resale/redistribution rights. Until this is clarified, commercial release is BLOCKED even though technical M0 work may continue.

## Runtime baseline

Known from current `develop/composer.json`:

- PHP: `>8.0 <8.5`
- curl
- dom
- gd
- mcrypt
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

- [ ] Confirm module installation/upgrade conventions
- [ ] Confirm available hooks/events for Turkey Edition features
- [ ] Confirm override conventions and limitations
- [ ] Confirm theme/template customization path
- [ ] Identify likely Turkey guest identity extension points
- [ ] Identify likely KBS integration extension points
- [ ] Identify payment provider extension points
- [ ] Identify SMS notification extension points
- [ ] Create `docs/CORE_PATCHES.md` if any unavoidable core change is identified

## Security / data baseline

- [ ] Identify where guest identity data is stored
- [ ] Identify authentication/session model
- [ ] Identify audit/logging capabilities
- [ ] Review file upload surfaces relevant to product use
- [ ] Review secrets/config storage method
- [ ] Record backup/restore baseline

## M0 closure rule

M0 may be marked **CLOSED** only when:

1. technical clean-install and core PMS smoke tests pass,
2. extension points are understood well enough to begin M1 without blind core edits,
3. license inventory is materially complete,
4. the `hotelreservationsystem` commercial-license blocker is resolved or an approved replacement strategy is documented,
5. `docs/AI_HANDOFF.md` contains the exact next step for M1.

Until then, status remains **IN PROGRESS**.
