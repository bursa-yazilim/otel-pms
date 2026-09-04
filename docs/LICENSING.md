# Licensing and Commercial Distribution Gate

## Status

**M0 commercial licensing review: IN PROGRESS / BLOCKING COMMERCIAL RELEASE**

This document is an engineering/commercial risk register, not legal advice. Bursa Yazılım must not assume that every file or module in the QloApps repository is governed by the same license merely because the root project metadata declares an open-source license.

Detailed first-pass findings are tracked in `docs/MODULE_LICENSE_INVENTORY.md`.

## Root project

The current QloApps root `composer.json` declares:

- package: `qloapps/qloapps`
- license: `OSL-3.0`

The current upstream README further states:

- QloApps Core is OSL-3.0,
- modules authored by Webkul use the applicable `LICENSE.md` kept in the module root,
- other modules are licensed under AFL-3.0.

This means module-level licensing must be reviewed separately.

## License inventory rule

Before commercial release, every first-party and bundled third-party module/component that will ship with the Bursa Yazılım product must be classified as one of:

- root/open-source license confirmed,
- separate compatible open-source license,
- separate commercial/proprietary license,
- license conflict / requires written clarification,
- license unclear / requires review,
- excluded from commercial distribution.

Do not infer module licensing from the root package or a single source-file header.

## Material M0 blocker: conflicting Webkul module licenses

The most important example is `hotelreservationsystem`.

Its main PHP source header states OSL-3.0, but `modules/hotelreservationsystem/LICENSE.md` contains a separate Webkul Software Licence Agreement.

That agreement includes, among other restrictions:

- use on one domain for the licensee's own use,
- no authorization to compile, copy or distribute the software or derivative works,
- no right to hand over, sell, distribute, sub-license, rent, lease or lend the software,
- restrictions related to derivative works and third-party development.

The same restrictive license text or the same type of header/license contradiction has also been observed during M0 in additional Webkul modules such as:

- `qlochannelmanagerconnector`,
- `qlohotelreview`,
- `qlopaypalcommerce`,
- `wkhotelroom`,
- `wkabouthotelblock`.

By contrast, `qlocrontaskmanager/LICENSE.md` explicitly states OSL-3.0, showing that module-root licenses are not uniform across the repository.

Because `hotelreservationsystem` describes itself as the backbone of QloApps booking processes, this is a **commercial distribution blocker until clarified**.

The existence of OSL source headers does not remove the risk because the QloApps README explicitly points Webkul modules to their module-root `LICENSE.md`.

Required resolution before a paid Bursa Yazılım release:

1. Determine why conflicting licensing texts are present in the public repository.
2. Obtain written clarification from QloApps/Webkul identifying the license that governs each conflicted Webkul module and the rights to modify, redistribute, host, white-label and resell it.
3. Preserve the written clarification in project/company records.
4. If redistribution under our intended model is not permitted, exclude or replace/reimplement affected capability using code we are legally allowed to distribute.
5. Have the final commercial model reviewed by qualified legal counsel before launch.

## Technical work while the gate is open

Technical exploration, clean-install testing and architecture work may continue.

However:

- do not describe the product as legally ready for resale,
- do not purchase a paid Webkul/QloApps addon and assume that purchase permits bundling it for every Bursa Yazılım customer,
- do not build new Turkey modules by copying code from a commercially unresolved Webkul module,
- use unresolved modules only as necessary for technical compatibility analysis until rights are clarified.

Where the platform exposes a generic extension contract, new Bursa modules should be implemented independently against that contract.

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
- [ ] exhaustive module/theme/third-party license inventory materially completed,
- [ ] `hotelreservationsystem` commercial rights clarified or an approved replacement strategy documented,
- [ ] other material conflicting Webkul module licenses classified,
- [ ] paid/hosted addon terms documented where relevant,
- [ ] intended Bursa Yazılım distribution/licensing model reviewed.

Technical exploration may continue while this gate is open, but the software must not be represented as ready for resale until the gate is resolved.
