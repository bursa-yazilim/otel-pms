# Licensing and Commercial Distribution Gate

## Status

**M0 commercial licensing review: IN PROGRESS / BLOCKING COMMERCIAL RELEASE**

This document is an engineering/commercial risk register, not legal advice. Bursa Yazılım must not assume that every file or module in the QloApps repository is governed by the same license merely because the root project metadata declares an open-source license.

## Root project

The current QloApps root `composer.json` declares:

- package: `qloapps/qloapps`
- license: `OSL-3.0`

This is the baseline license declaration for the root package.

## License inventory rule

Before commercial release, every first-party and bundled third-party module/component that will ship with the Bursa Yazılım product must be classified as one of:

- root/open-source license confirmed,
- separate compatible open-source license,
- separate commercial/proprietary license,
- license unclear / requires clarification,
- excluded from commercial distribution.

Do not infer module licensing from the root package.

## Known M0 blocker: `hotelreservationsystem`

`modules/hotelreservationsystem/LICENSE.md` contains a separate Webkul Software Licence Agreement.

The text includes, among other restrictions:

- use on one domain for the licensee's own use,
- no authorization to compile, copy or distribute the software or derivative works,
- no right to hand over, sell, distribute, sub-license, rent, lease or lend the software,
- restrictions related to derivative works and third-party development.

Because the hotel reservation module is central to the intended product, this is a **commercial distribution blocker until clarified**.

Required resolution before a paid Bursa Yazılım release:

1. Determine why this separately licensed file is included in the public QloApps repository.
2. Determine whether another project-level license notice supersedes or legally covers this module.
3. Obtain written clarification/permission from QloApps/Webkul if necessary.
4. If redistribution under our intended model is not permitted, replace/reimplement the affected capability using code we are legally allowed to distribute.
5. Have the planned commercial model reviewed by qualified legal counsel before launch.

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

## Bursa Yazılım proprietary modules

Where legally possible, Turkey-specific modules developed entirely by Bursa Yazılım should be kept logically separate from upstream code to make ownership and licensing boundaries explicit.

Examples:

- Turkey KBS integration,
- Netgsm provider,
- Turkey payment provider modules,
- Bursa licensing client,
- product-specific theme/branding,
- Turkey-specific reporting and operational features.

Whether a proprietary module may remain closed when interacting with OSL/GPL-like code must be evaluated against the applicable license and method of linking/derivation; do not assume separation alone guarantees this.

## M0 licensing exit gate

M0 cannot be marked CLOSED for commercial-product purposes until:

- [ ] root license reviewed,
- [ ] module license inventory completed,
- [ ] `hotelreservationsystem` commercial rights clarified,
- [ ] bundled third-party licenses inventoried,
- [ ] paid/hosted addon terms documented where relevant,
- [ ] intended Bursa Yazılım distribution/licensing model reviewed.

Technical exploration may continue while this gate is open, but the software must not be represented as ready for resale until the gate is resolved.
