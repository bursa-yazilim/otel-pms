# Module License Inventory

## Status

**M0 first-pass inventory — IN PROGRESS**

This file records the license evidence found in the current upstream baseline. It is an engineering/commercial risk inventory, not legal advice and not yet an exhaustive legal review.

Baseline commit:

`7318ae2c0056e1e0d4167424c942a28053ad1b08`

## Project-level rule stated by upstream

The current QloApps README states:

- QloApps Core is licensed under OSL-3.0.
- Modules authored by Webkul use the applicable `LICENSE.md` located in the module root.
- Other modules are licensed under AFL-3.0.

Therefore module-level `LICENSE.md` files take material importance for the commercial distribution review. A source-file header alone must not be used to override a conflicting module-root license without written clarification.

## First-pass findings

| Component | Evidence observed | Current M0 classification | Action |
| --- | --- | --- | --- |
| QloApps root/core | Root `composer.json` declares OSL-3.0; README states core OSL-3.0 | OSL-3.0 baseline | Full OSL obligations review before commercial release |
| `hotelreservationsystem` | Main PHP header says OSL-3.0, but module-root `LICENSE.md` contains Webkul Software Licence Agreement restricting redistribution/derivatives | **CONFLICT / BLOCKER** | Written clarification required; do not assume resale rights |
| `qlochannelmanagerconnector` | Main PHP header says OSL-3.0, module-root `LICENSE.md` contains restrictive Webkul agreement | **CONFLICT / BLOCKER for bundled redistribution** | Treat connector/provider terms separately; obtain clarification |
| `qlohotelreview` | Module-root `LICENSE.md` contains restrictive Webkul agreement | **RESTRICTIVE / REVIEW REQUIRED** | Confirm whether it may ship in Bursa product |
| `qlopaypalcommerce` | Main PHP header says OSL-3.0, module-root `LICENSE.md` contains restrictive Webkul agreement | **CONFLICT / REVIEW REQUIRED** | Do not rely on header alone |
| `wkhotelroom` | Module-root `LICENSE.md` contains restrictive Webkul agreement | **RESTRICTIVE / REVIEW REQUIRED** | Clarify before redistribution |
| `wkabouthotelblock` | Module-root `LICENSE.md` contains restrictive Webkul agreement | **RESTRICTIVE / REVIEW REQUIRED** | Clarify before redistribution |
| `qlocrontaskmanager` | Module-root `LICENSE.md` explicitly states OSL-3.0 | OSL-3.0 observed | Keep license notice/obligations; legal review still required |
| `qloduitkupayment` | Main PHP header states AFL-3.0; referenced module-root `LICENSE.md` is not present at expected path | **AFL-3.0 header / PACKAGE REVIEW REQUIRED** | Verify all bundled files/dependencies and missing license reference |
| `qloicsexport` | Module exists; expected `LICENSE.md` not found during first pass | **UNKNOWN / REVIEW REQUIRED** | Inspect file headers/package metadata |
| PrestaShop-derived/core bundled modules | Upstream README says non-Webkul modules are AFL-3.0; individual files may retain upstream notices | **AFL-3.0 expected** | Inventory exceptions and bundled third-party licenses |

## Important contradiction found

Several Webkul-authored modules contain two different-looking licensing signals:

1. PHP file header says the source file is OSL-3.0.
2. The same module's root `LICENSE.md` is a Webkul Software Licence Agreement that restricts copying, distribution, resale, sublicensing and derivative works.

Because the QloApps README explicitly directs readers to each Webkul module's root `LICENSE.md`, this is not safe to dismiss as a harmless stale file.

Until Webkul/QloApps gives a written interpretation, Bursa Yazılım must treat these components as commercially unresolved.

## Commercial implications for product architecture

The Turkey Edition should not become unnecessarily dependent on unresolved modules when a clean independent integration can be created.

Examples:

- Turkey payment provider: create a new Bursa module using documented platform payment extension points rather than modifying a Webkul payment module.
- SMS/KBS: new Bursa-owned modules.
- Branding/theme: Bursa-owned theme/customization layer where the applicable upstream theme license permits it.
- Channel Manager: keep provider/connector boundary replaceable; do not assume the bundled connector can be resold.

The central booking/reservation functionality is different: `hotelreservationsystem` is described by QloApps itself as the backbone of the booking process, so its license conflict must be resolved before a commercial product based on the full current distribution can be declared sale-ready.

## Remaining inventory work

- [ ] Enumerate every directory under `modules/` and classify author/license.
- [ ] Inspect all module-root `LICENSE`, `LICENSE.md`, `LICENSE.txt`, composer/package metadata and source headers.
- [ ] Inventory `themes/` licenses.
- [ ] Inventory bundled JS/PHP libraries under `tools/`, `vendor`-like locations and module dependencies.
- [ ] Identify assets/fonts/images with separate redistribution terms.
- [ ] Record hosted/service terms separately from source-code licenses.
- [ ] Obtain written QloApps/Webkul clarification for conflicting Webkul module licenses.
- [ ] Obtain qualified legal review for Bursa Yazılım's intended resale/license model before launch.

## M0 rule

This inventory can become more detailed during later technical work, but M0 cannot close while the core booking module's commercial status is unresolved.
