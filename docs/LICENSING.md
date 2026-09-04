# Licensing and Commercial Distribution Gate

## Status

**M0 commercial licensing review: IN PROGRESS / BLOCKING COMMERCIAL RELEASE**

This document is an engineering/commercial risk register, not legal advice. Bursa Yazılım must not assume that every file or module in the QloApps repository is governed by the same license merely because the root project metadata declares an open-source license.

Detailed findings and Bursa product decisions are tracked in `docs/MODULE_LICENSE_INVENTORY.md`.

## Root project

The current QloApps root `composer.json` declares:

- package: `qloapps/qloapps`
- license: `OSL-3.0`

The current upstream README further states:

- QloApps Core is OSL-3.0,
- modules authored by Webkul use the applicable license kept in the module root,
- other modules are licensed under AFL-3.0.

This means module-level licensing must be reviewed separately.

## License inventory rule

Before commercial release, every first-party and bundled third-party module/component that will intentionally ship with the Bursa Yazılım product must be classified as one of:

- root/open-source license confirmed,
- separate compatible open-source license,
- separate commercial/proprietary license,
- license conflict / requires written clarification,
- license unclear / requires review,
- customer-licensed/external provider,
- Bursa independent reimplementation candidate,
- excluded from commercial distribution.

Do not infer module licensing from the root package or from a single source-file header.

## Material M0 blocker: conflicting Webkul module licenses

The most important example is `hotelreservationsystem`.

Its main PHP source header states OSL-3.0, but `modules/hotelreservationsystem/LICENSE.md` contains a separate Webkul Software Licence Agreement.

That agreement includes, among other restrictions:

- use on one domain for the licensee's own use,
- no authorization to compile, copy or distribute the software or derivative works,
- no right to hand over, sell, distribute, sub-license, rent, lease or lend the software,
- restrictions related to derivative works and third-party development.

The same restrictive agreement or the same kind of package/header contradiction has now been directly observed during M0 in:

- `hotelreservationsystem`,
- `qlochannelmanagerconnector`,
- `qlohotelreview`,
- `qlopaypalcommerce`,
- `wkhotelroom`,
- `wkabouthotelblock`,
- `qloduitkupayment`.

`qloduitkupayment` is especially useful evidence of the contradiction pattern: its main PHP file explicitly declares AFL-3.0 and says the AFL license is bundled as `LICENSE.md`, while the actual package contains `LICENSE.txt` with the restrictive Webkul Software Licence Agreement. Therefore neither an OSL nor AFL source header can automatically settle a conflicting module package license.

By contrast, `qlocrontaskmanager/LICENSE.md` explicitly states OSL-3.0, showing that module-root license evidence is not uniform across the repository.

`qloicsexport` currently has an AFL-3.0 source header but the referenced module-root `LICENSE.md` is absent, so it remains a package-review item rather than a known restrictive module.

Because `hotelreservationsystem` is the core reservation/PMS backbone, its commercial status remains a **commercial distribution blocker until clarified**.

Required resolution before a paid Bursa Yazılım release:

1. Determine why conflicting licensing texts are present in the public repository.
2. Obtain written clarification from QloApps/Webkul identifying the license that governs each commercially material conflicted Webkul module and the rights to modify, redistribute, host, white-label and resell it.
3. Specifically confirm multiple-customer installations and recurring Bursa Yazılım license/subscription fees.
4. Preserve the written clarification in project/company records.
5. If redistribution under our intended model is not permitted, exclude or independently replace/reimplement affected noncritical capability using code/interfaces we are legally allowed to use.
6. If the core `hotelreservationsystem` cannot be redistributed under our model, perform a formal go/no-go comparison before further major QloApps-specific investment.
7. Have the final commercial model reviewed by qualified legal counsel before launch.

Exact clarification questions are maintained in `docs/COMMERCIAL_LICENSE_CLARIFICATION.md`.

## Technical work while the gate is open

Technical exploration, clean-install testing and architecture work may continue.

However:

- do not describe the product as legally ready for resale,
- do not purchase a paid Webkul/QloApps addon and assume that purchase permits bundling it for every Bursa Yazılım customer,
- do not build new Turkey modules by copying code from a commercially unresolved Webkul module,
- use unresolved modules only as necessary for technical compatibility analysis until rights are clarified,
- preserve upstream `develop`; exclusion from a Bursa commercial build does not mean deleting upstream code/history.

Where the platform exposes a generic extension contract, new Bursa modules should be implemented independently against that contract.

## Current Bursa decision by capability

### Reservation / PMS backbone

`hotelreservationsystem` must receive written commercial clarification. This is the principal M0 license gate.

### Channel Manager

Do not assume `qlochannelmanagerconnector` can be bundled into every Bursa installation. Initial commercial architecture should treat channel management as a separately licensed customer/provider service unless written redistribution rights say otherwise.

### Reviews and presentation blocks

If required, prefer independent Bursa implementations over dependence on restrictive `qlohotelreview`, `wkabouthotelblock` or similar presentation modules.

### Turkey payments

Do not base PayTR/iyzico work on unresolved Webkul payment module source. Implement Bursa provider modules independently against permitted payment extension points. `qlopaypalcommerce` and `qloduitkupayment` are not required for the initial Turkey MVP.

### Cron

`qlocrontaskmanager` currently has explicit OSL-3.0 module-root evidence and may be used subject to license obligations and runtime validation.

## Paid QloApps add-ons

Commercial add-ons purchased from qloapps.com are not automatically assumed to be redistributable inside our product.

For each paid module or hosted service, separately record:

- license scope,
- domain/installation limits,
- whether resale is allowed,
- whether white-labeling is allowed,
- whether the end customer must purchase directly,
- recurring provider cost,
- termination/update conditions.

## Third-party services

External integrations such as Booking.com, Airbnb, Expedia, Meta/WhatsApp, iyzico, PayTR, Netgsm and KBS have their own contracts, API terms and eligibility rules. Open-source status of the PMS does not grant access or redistribution rights to those services.

## Bursa Yazılım-owned modules

Where legally possible, Turkey-specific modules developed independently by Bursa Yazılım should be kept logically separate from upstream code to make ownership and licensing boundaries explicit.

Examples:

- Turkey KBS integration,
- Netgsm provider,
- Turkey payment provider modules,
- Bursa licensing client,
- product-specific theme/branding,
- Turkey-specific reporting and operational features.

Whether a Bursa-owned module may remain under a proprietary license while interacting with OSL/AFL or another module must be evaluated against the actual applicable license and implementation relationship. Do not assume separation alone guarantees a particular licensing result.

## M0 licensing exit gate

M0 cannot be marked CLOSED for commercial-product purposes until:

- [x] root license declaration reviewed,
- [x] upstream module-license rule identified,
- [x] first-pass conflicting/restrictive module examples inventoried,
- [x] practical Bursa handling strategy defined for the currently identified noncritical restrictive modules,
- [ ] exhaustive/material module-theme-third-party license inventory completed,
- [ ] `hotelreservationsystem` commercial rights clarified or an approved replacement/go-no-go strategy documented,
- [ ] remaining commercially material conflicting Webkul module licenses classified,
- [ ] paid/hosted addon terms documented where relevant,
- [ ] intended Bursa Yazılım distribution/licensing model reviewed.

Technical exploration may continue while this gate is open, but the software must not be represented as ready for resale until the gate is resolved.