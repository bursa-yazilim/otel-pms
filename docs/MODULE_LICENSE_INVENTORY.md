# Module License Inventory

## Status

**M0 first-pass inventory — IN PROGRESS**

This file records license evidence found in the current upstream baseline and the corresponding Bursa Yazılım product decision. It is an engineering/commercial risk inventory, not legal advice and not yet an exhaustive legal review.

Baseline commit:

`7318ae2c0056e1e0d4167424c942a28053ad1b08`

## Project-level rule stated by upstream

The current QloApps README states:

- QloApps Core is licensed under OSL-3.0.
- Modules authored by Webkul use the applicable license file located in the module root.
- Other modules are licensed under AFL-3.0.

Therefore module-level `LICENSE`, `LICENSE.md` and `LICENSE.txt` files take material importance for commercial distribution review. A source-file header alone must not be used to override a conflicting module-root license without written clarification.

## Decision classes

| Decision | Meaning |
| --- | --- |
| **USE** | License evidence is compatible enough for technical/product planning; obligations still apply. |
| **WRITTEN CLARIFICATION REQUIRED** | Conflicting or restrictive license evidence prevents bundled commercial redistribution from being assumed. |
| **CUSTOMER-LICENSE / EXTERNAL SERVICE** | Do not bundle provider rights into Bursa license; customer/provider relationship is handled separately. |
| **BURSA REIMPLEMENTATION CANDIDATE** | If required, implement independently against permitted platform extension points without copying unresolved module code. |
| **EXCLUDE FROM COMMERCIAL ARTIFACT** | Preserve in upstream `develop`, but do not intentionally distribute/enable in Bursa commercial build unless rights are resolved. |
| **PACKAGE REVIEW REQUIRED** | Source header suggests an open-source license but package-level evidence is incomplete or inconsistent. |

## Critical findings and Bursa decisions

| Component | Function / importance | Evidence observed | Current M0 classification | Bursa commercial decision |
| --- | --- | --- | --- | --- |
| QloApps root/core | Platform core | Root `composer.json` declares OSL-3.0; README states core OSL-3.0 | **OSL-3.0 baseline** | **USE**, subject to final OSL obligations review |
| `hotelreservationsystem` | Core hotel reservation/PMS backbone | Main PHP header says OSL-3.0, but module-root `LICENSE.md` contains restrictive Webkul Software Licence Agreement covering one-domain use and restricting distribution/derivatives | **CONFLICT / RELEASE BLOCKER** | **WRITTEN CLARIFICATION REQUIRED**. If redistribution rights are denied, stop and compare independent reservation-layer reimplementation versus replacing QloApps as the product base |
| `qlochannelmanagerconnector` | Channel-manager connector / OTA boundary | Main PHP header says OSL-3.0; module-root `LICENSE.md` contains restrictive Webkul agreement | **CONFLICT / BLOCKER FOR BUNDLING** | Prefer **CUSTOMER-LICENSE / EXTERNAL SERVICE** initially. Do not assume this connector can be bundled for all Bursa customers |
| `qlohotelreview` | Hotel reviews | Module-root `LICENSE.md` contains restrictive Webkul agreement | **RESTRICTIVE / REVIEW REQUIRED** | **BURSA REIMPLEMENTATION CANDIDATE** if review functionality is required in the commercial product |
| `qlopaypalcommerce` | PayPal payment integration | Main PHP header says OSL-3.0; module-root `LICENSE.md` contains restrictive Webkul agreement | **CONFLICT / REVIEW REQUIRED** | Not required for Turkey MVP. **EXCLUDE FROM COMMERCIAL ARTIFACT** if unresolved; implement PayTR/iyzico independently instead |
| `wkhotelroom` | Hotel-room related front-office functionality | Module-root `LICENSE.md` contains restrictive Webkul agreement | **RESTRICTIVE / REVIEW REQUIRED** | Determine dependency on core booking flow. If nonessential, exclude/replace; if essential, include in Webkul written clarification request |
| `wkabouthotelblock` | Hotel/about presentation block | Module-root `LICENSE.md` contains restrictive Webkul agreement | **RESTRICTIVE / REVIEW REQUIRED** | **BURSA REIMPLEMENTATION CANDIDATE** / product theme responsibility; do not depend on it for commercial branding |
| `qlocrontaskmanager` | Scheduled/cron task management | Module-root `LICENSE.md` explicitly states OSL-3.0 | **OSL-3.0 observed** | **USE** if runtime tests validate it; retain required notices/obligations |
| `qloduitkupayment` | Duitku payment integration | Main PHP header explicitly says AFL-3.0 and claims an AFL `LICENSE.md`; package actually contains `LICENSE.txt` whose blob/content is the restrictive Webkul Software Licence Agreement | **LICENSE CONFLICT / REVIEW REQUIRED** | Not relevant to Turkey MVP. Preserve in upstream `develop` but **EXCLUDE FROM COMMERCIAL ARTIFACT** while unresolved |
| `qloicsexport` | ICS/iCalendar export | Main PHP header explicitly states AFL-3.0 and references `LICENSE.md`; expected module-root `LICENSE.md` is not present in current package | **AFL-3.0 HEADER / PACKAGE REVIEW REQUIRED** | Potentially usable after package-license notice is clarified; no need to block Turkey MVP on this module |
| PrestaShop-derived/core bundled modules | Legacy/general platform modules | Upstream README says non-Webkul modules are AFL-3.0; individual files may retain upstream notices | **AFL-3.0 expected** | Continue inventory for exceptions and bundled third-party licenses |

## Important contradiction pattern

Several Webkul-authored modules contain two different licensing signals:

1. a PHP source-file header states OSL-3.0 or AFL-3.0, while
2. the same module package contains a Webkul Software Licence Agreement restricting copying, distribution, resale, sublicensing and derivative works.

`qloduitkupayment` confirms that the conflict is not limited to modules whose PHP headers say OSL-3.0: its main PHP file states AFL-3.0 while its bundled `LICENSE.txt` contains the restrictive Webkul agreement.

Because QloApps itself directs Webkul modules to their module-level licenses, Bursa Yazılım must not silently choose the more permissive header. Written clarification is required where the commercial product would depend on a conflicted component.

## Commercial architecture consequences

The Turkey Edition should avoid unnecessary dependency on commercially unresolved modules when a clean independent integration can be created.

Preferred direction:

- **Reservation/PMS backbone:** resolve `hotelreservationsystem` first; this is the strategic go/no-go item.
- **Channel Manager:** initially treat as a separately licensed provider/service per customer rather than Bursa-bundled code.
- **Turkey payments:** independent Bursa PayTR/iyzico modules against permitted QloApps payment extension points; do not fork `qlopaypalcommerce` or `qloduitkupayment` code.
- **Reviews:** independent Bursa review module if needed.
- **SMS/KBS:** Bursa-owned modules.
- **Branding/about blocks:** Bursa-owned theme/modules rather than dependence on restrictive presentation modules.
- **Cron:** `qlocrontaskmanager` may remain where its OSL-3.0 status and runtime compatibility are confirmed.

Independent reimplementation means implementing product requirements from our own specification against legally usable platform interfaces. It does not mean copying, translating or lightly modifying code from an unresolved Webkul module.

## Upstream preservation rule

A decision to exclude a module from the Bursa commercial artifact does **not** mean deleting it from QloApps upstream history.

- `develop` remains the upstream tracking branch and preserves upstream capabilities.
- Commercial packaging/enablement decisions belong to Bursa product/release branches.
- A currently unused capability must not be casually removed because a future customer may require it.

## Remaining inventory work

- [ ] Enumerate every directory under `modules/` and classify author/license or inheritance rule.
- [ ] Inspect remaining module-root `LICENSE`, `LICENSE.md`, `LICENSE.txt`, package metadata and material source headers.
- [ ] Determine whether `wkhotelroom` is technically required by the core reservation flow or replaceable presentation functionality.
- [ ] Inventory `themes/` licenses and branding assets.
- [ ] Inventory bundled JS/PHP libraries under `tools/`, vendor-like locations and module dependencies.
- [ ] Identify assets/fonts/images with separate redistribution terms.
- [ ] Record paid addon/hosted-service terms separately from source-code licenses.
- [ ] Obtain written QloApps/Webkul clarification for `hotelreservationsystem` and other commercially material conflicts.
- [ ] Obtain qualified legal review for Bursa Yazılım's final intended resale/license model before launch.

## M0 rule

This inventory can become more detailed during later technical work, but M0 cannot close while the core booking module's commercial status is unresolved. Noncritical modules with a documented exclusion/replacement strategy do not individually need to block technical M0 progress.