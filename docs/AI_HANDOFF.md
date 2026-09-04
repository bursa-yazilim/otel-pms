# AI / Developer Handoff

## Project

Repository: `bursa-yazilim/otel-pms`

Goal: productize the current QloApps codebase for the Turkish hospitality market, initially targeting small/boutique accommodation businesses.

## Branches

- `develop`: upstream QloApps tracking branch. Do not add product-specific changes here.
- `main`: Bursa Yazılım product integration branch.
- working branches: branch from `main`, merge back by PR.

Current M0 working branch:

`chore/m0-foundation`

## Upstream baseline

Initial source commit:

`7318ae2c0056e1e0d4167424c942a28053ad1b08`

The separately downloaded QloApps 1.7.0 ZIP is intentionally excluded from the project workflow. Do not replace repository files with that ZIP.

## Current milestone

M0 — Foundation, upstream and commercial viability

Status: **IN PROGRESS**

Read these files before starting project work:

1. `docs/AI_HANDOFF.md`
2. `docs/ARCHITECTURE.md`
3. `docs/ROADMAP.md`
4. `docs/QLOAPPS_UPSTREAM.md`
5. `docs/LICENSING.md`
6. `docs/TURKEY_REQUIREMENTS.md`
7. `docs/M0_CHECKLIST.md`
8. upstream root `AGENTS.md`

## Non-negotiable project rules

### Preserve upstream tracking

Do not commit Bursa Yazılım features directly to `develop`.

### Do not delete future capability casually

An upstream feature that is unnecessary today may be required by a future hotel/customer. Prefer hiding, configuration, permissions, or feature flags over deletion.

### Extension first

Prefer:

1. module,
2. hooks/events,
3. overrides,
4. themes/templates,
5. core changes only when unavoidable.

Document unavoidable core changes.

### Licensing is a release gate

Do not state that the product can legally be resold merely because QloApps root metadata declares OSL-3.0.

A known blocker exists at:

`modules/hotelreservationsystem/LICENSE.md`

It contains a separate restrictive Webkul software license. Commercial rights must be clarified before the product is represented as sale-ready.

### No invented API assumptions

Especially for KBS, do not assume a public REST API. Verify the official integration method and authentication requirements before designing the final adapter.

### Protect sensitive data

Never commit:

- real TCKN/passport data,
- real guest records,
- production API keys,
- database passwords,
- payment secrets,
- KBS credentials,
- SMS/WhatsApp secrets.

Use environment/configuration mechanisms appropriate to the QloApps architecture.

### Keep integrations replaceable

Turkey-specific providers such as SMS/payment should be behind provider/service boundaries so the product is not locked to one provider unnecessarily.

## Current product priorities

Saleable MVP priorities:

1. professional Turkish localization,
2. operational PMS UX,
3. multi-guest identity model,
4. KBS,
5. one Turkish payment provider,
6. Netgsm,
7. Turkish direct booking engine.

Do not block first pilot on building our own OTA channel manager.

## Technical baseline known at M0 start

Current `develop` `composer.json` declares PHP `>8.0 <8.5` and required extensions including curl, dom, gd, mcrypt, openssl, PDO MySQL, phar, simplexml, soap and zip.

This requirement must be validated with an actual clean installation before M0 closes.

## M0 exact next work

1. Complete module/license inventory.
2. Determine the commercial status of `hotelreservationsystem` and any other separately licensed modules.
3. Establish a clean local test environment using a supported PHP version.
4. Perform clean install.
5. Perform admin login smoke test.
6. Perform direct booking/reservation smoke test.
7. Perform check-in/check-out baseline smoke test.
8. Record database/runtime requirements and installer findings.
9. Identify core files that Turkey Edition is likely to need to modify; first attempt module/override alternatives.
10. Update `docs/M0_CHECKLIST.md` and this handoff after each material finding.

## Handoff update rule

At the end of every milestone:

- update roadmap milestone status,
- record completed code and architecture decisions,
- record tests run and results,
- record known bugs/blockers,
- update exact next step,
- do not mark a milestone CLOSED while a documented exit criterion remains unresolved.
