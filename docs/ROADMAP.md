# Otel PMS Roadmap

## Product goal

Turn the current QloApps `develop` codebase into a Turkey-focused, commercially supportable PMS for small and boutique accommodation businesses while retaining upstream compatibility.

## M0 — Foundation, upstream and commercial viability

**Status: IN PROGRESS**

Scope:

- establish branch model,
- freeze/document upstream baseline,
- define extension-first architecture,
- define Turkey Edition requirements,
- inventory licenses and commercial-distribution risks,
- define M0 smoke-test environment,
- validate clean install/admin/booking baseline,
- identify unavoidable core customization points.

Exit criteria:

- [x] current upstream/fork baseline confirmed,
- [x] `develop` reserved for upstream tracking,
- [x] `main` product branch created,
- [x] M0 architecture/upstream documentation created,
- [x] Turkey requirements documented,
- [x] known licensing blocker documented,
- [ ] complete module/third-party license inventory,
- [ ] resolve/clarify `hotelreservationsystem` commercial redistribution rights,
- [ ] clean install on selected supported local PHP/MySQL stack,
- [ ] admin login smoke test,
- [ ] reservation/booking smoke test,
- [ ] check-in/check-out baseline smoke test,
- [ ] record current database/runtime requirements,
- [ ] create core customization map,
- [ ] M0 final review.

M0 is not CLOSED until both technical baseline and commercial licensing gate are acceptable.

## M1 — Product identity and Turkish localization

- Bursa Yazılım/product branding layer,
- Turkish terminology audit,
- Turkish locale defaults,
- TL/date/time/address defaults,
- initial theme/admin branding,
- no destructive removal of upstream features.

## M2 — PMS operational UX

- simplify daily navigation,
- dashboard for arrivals/departures/occupancy/balances,
- improve room calendar usability,
- role/permission based menu simplification,
- preserve advanced upstream functions behind configuration where possible.

## M3 — Turkey guest identity model

- reservation holder vs staying guests,
- multiple guests per reservation,
- TCKN/passport/nationality fields,
- validation and privacy/masking rules,
- audit requirements.

## M4 — KBS integration

- confirm official integration method,
- Turkey KBS module,
- validation,
- send/retry/status flow,
- audit/error logs,
- operational KBS dashboard.

## M5 — Turkey payment provider

- select iyzico or PayTR,
- deposit/full payment,
- outstanding balance,
- callback/webhook verification,
- refund/cancellation flow,
- no raw card storage.

## M6 — Turkey SMS provider

- provider abstraction,
- Netgsm integration,
- reservation/arrival/payment notification events,
- message templates and logs.

## M7 — Direct booking engine Turkey Edition

- professional Turkish booking flow,
- mobile usability,
- payment integration,
- optional extras,
- confirmation flow,
- website link/embed strategy.

At the end of M7 the product should be capable of entering controlled pilot use, subject to the commercial licensing gate being resolved.

## M8 — Commercial platform foundations

- Bursa license client/entitlements,
- installer/deployment workflow,
- backup/restore,
- audit/security hardening,
- update strategy,
- customer-specific configuration separation.

## M9 — Pilot readiness

- demo property/data,
- help center baseline,
- onboarding checklist,
- support diagnostics,
- pilot agreement/process,
- monitoring and error reporting.

## M10 — Pilot stabilization

Pilot with 3–5 properties representing multiple property types.

Classify findings as:

- bug,
- common product requirement,
- customer-specific customization.

Do not turn every pilot request into core product scope.

## M11 — OTA / Channel Manager

- initially integrate an approved existing channel manager/provider,
- map room/rate/availability/reservation states,
- document recurring third-party cost,
- evaluate independent channel manager only after product traction.

## M12 — WhatsApp and advanced communication

- WhatsApp Business integration,
- transactional templates,
- pre-arrival/post-stay automation,
- provider cost and consent handling.

## M13 — Turkish invoicing/accounting bridge

- choose first supported provider/integrator,
- e-Fatura/e-Arşiv bridge where commercially justified,
- export/accounting interoperability,
- avoid building a full accounting ERP inside PMS.

## M14 — Advanced reporting / PWA

- owner KPIs,
- mobile/PWA housekeeping and front-desk views,
- operational analytics,
- performance optimization.

## Scope control principles

1. Sellable operational value beats feature count.
2. Do not remove existing upstream capability solely because it is not in the MVP.
3. Turkey-specific integrations should be replaceable provider modules where possible.
4. Upstream compatibility is a standing requirement.
5. Commercial/legal rights are release gates, not documentation footnotes.
