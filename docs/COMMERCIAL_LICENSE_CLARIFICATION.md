# Commercial License Clarification Request

## Purpose

This document records the exact commercial licensing questions that must be answered before Bursa Yazılım represents the QloApps-based product as ready for paid redistribution, white-labeling or customer installation.

This is an engineering/commercial due-diligence checklist, not legal advice.

## Context

Repository baseline:

`7318ae2c0056e1e0d4167424c942a28053ad1b08`

The QloApps root package declares OSL-3.0 and the upstream README states that Webkul-authored modules use the applicable `LICENSE.md` in each module root.

However, important Webkul modules contain restrictive module-root license text that appears inconsistent with OSL-3.0 source headers.

The most important example is:

`modules/hotelreservationsystem/LICENSE.md`

This module is central to hotel booking operations and its license text includes restrictions concerning one-domain use, copying, distribution, sale, sublicensing and derivative works.

## Questions requiring written clarification from QloApps / Webkul

1. Which license legally governs `modules/hotelreservationsystem` in the public QloApps GitHub repository: the OSL-3.0 source-file headers or the module-root Webkul Software Licence Agreement?
2. May Bursa Yazılım modify `hotelreservationsystem` for a Turkey-specific distribution?
3. May Bursa Yazılım redistribute that modified module to paying customers?
4. May Bursa Yazılım install the resulting product on multiple independent customer domains/installations?
5. May Bursa Yazılım white-label the user interface and sell implementation, maintenance and support under its own product brand while preserving required copyright/license notices?
6. If customer-by-customer licensing is required, what exact license must each customer obtain and at what scope?
7. Are derivative works or extensions that integrate with `hotelreservationsystem` required to use a specific license?
8. Does the same answer apply to other bundled Webkul modules whose root `LICENSE.md` uses the restrictive Webkul Software Licence Agreement?
9. Which bundled modules are explicitly intended to be freely redistributable as part of the open-source QloApps distribution?
10. Are there any trademark/branding restrictions on removing QloApps/Webkul branding from the user interface while preserving legal notices in source/distribution documentation?

## Modules currently requiring the same classification review

- `hotelreservationsystem`
- `qlochannelmanagerconnector`
- `qlohotelreview`
- `qlopaypalcommerce`
- `wkhotelroom`
- `wkabouthotelblock`

This list is not yet exhaustive.

## Required evidence

Before commercial release, preserve one of the following in Bursa Yazılım company/project records:

- written clarification from an authorized QloApps/Webkul representative,
- an updated official license file/README that removes the contradiction,
- or a qualified legal opinion plus an approved technical replacement strategy for unresolved components.

A verbal statement or forum comment is not sufficient for the commercial release gate.

## Product decision until resolved

Technical development may continue, but:

- do not market the product as legally ready for resale,
- do not copy implementation code from unresolved proprietary/restrictive modules into new Bursa-owned modules,
- do not purchase a paid add-on and assume that purchase permits bundling it for all Bursa Yazılım customers,
- keep Turkey-specific integrations independently implemented behind module/provider boundaries,
- preserve an option to replace commercially unresolved modules if necessary.

## M0 impact

This clarification is a blocking exit criterion for M0 commercial viability. M0 technical work can continue in parallel, but M0 must not be marked CLOSED for commercial release until this issue is resolved or an approved replacement strategy is documented.
