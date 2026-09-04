# Otel PMS Architecture

## Status

M0 foundation document. The product is based on the current `develop` branch of upstream QloApps and will be extended for the Turkish hospitality market.

## Repository and branch model

- Upstream source: `Qloapps/QloApps`
- Product fork: `bursa-yazilim/otel-pms`
- `develop`: upstream tracking branch. Product-specific development must not be committed directly here.
- `main`: Bursa Yazılım product branch.
- Short-lived branches: `feature/*`, `fix/*`, `chore/*` branching from `main` and merged back by PR.

## Baseline

The initial fork baseline is upstream commit:

`7318ae2c0056e1e0d4167424c942a28053ad1b08`

The downloadable QloApps 1.7.0 ZIP is not a project source of truth. It corresponds to an older `v1.7.x` code line. The forked `develop` branch is the only upstream baseline used by this project.

## Extension-first policy

Product development should preserve upstream QloApps functionality wherever practical.

Order of preference for customization:

1. New module
2. Existing QloApps hook/event integration
3. Override
4. Product theme/template customization
5. Core modification only when the previous approaches cannot solve the requirement

Every unavoidable core modification must be documented with:

- affected file/path,
- reason,
- upstream baseline,
- compatibility impact,
- expected merge conflict risk.

Existing QloApps functionality must not be removed merely because it is not required by the current MVP. Prefer configuration, permissions, navigation hiding, or feature flags so later customer requirements can reuse upstream capability.

## Product layers

```text
QloApps Core
    |
    +-- Bursa Hotel Core
    +-- Turkey Localization
    +-- Turkey Guest Identity
    +-- Turkey KBS
    +-- Turkey SMS
    +-- Turkey Payment
    +-- Turkey Invoice / Accounting Bridge
    +-- Bursa License Client
    +-- Bursa Theme
```

### Bursa Hotel Core

Shared product-level configuration and integrations that are not specific to one Turkish provider. It should avoid becoming a monolithic replacement for QloApps core.

### Turkey Localization

Professional Turkish UI, Turkish currency/date/time conventions, address structure, local terminology, and market-specific defaults.

### Turkey Guest Identity

Supports reservation holder and all staying guests separately. Turkish and foreign guest identity records must support TCKN/passport, nationality and fields required by legal integrations.

### Turkey KBS

KBS integration must be isolated behind a module/service boundary. Do not assume a public REST API. The supported official integration method must be validated before implementation is locked.

### Turkey SMS

Provider abstraction. Netgsm is the initial preferred provider; additional providers can be added without changing booking business logic.

### Turkey Payment

Provider abstraction. First production provider will be selected between iyzico and PayTR. Card data must not be stored or processed directly by Otel PMS when hosted payment/tokenized provider flows are available.

### Bursa License Client

Licensing will be integrated only after the product entitlement model is defined. License failure must not abruptly block hotel front-desk operations; grace/read-only behavior will be designed before activation.

## Initial deployment model

For the first commercial phase, prefer one application/database installation per customer/property rather than converting QloApps immediately into a shared-database multi-tenant SaaS.

Benefits:

- simpler data isolation,
- lower migration risk,
- easier backup/restore,
- easier customer export,
- reduced blast radius,
- less invasive changes to upstream QloApps.

A true multi-tenant SaaS architecture can be evaluated after product-market fit and operational experience.

## Sensitive data

The application may process TCKN, passport information and stay records. These fields are treated as sensitive operational data even when not all are legally classified in the same category.

Minimum architectural rules:

- least-privilege access,
- auditability for sensitive actions,
- no credentials/secrets in Git,
- encrypted transport,
- defined backup and retention policy,
- explicit deletion/retention rules,
- masked sensitive identifiers where full display is unnecessary.

## Architecture decision rule

When a requirement can be implemented without modifying upstream core, that approach is preferred even if the initial implementation is slightly more work. Long-term upstream compatibility is a product requirement, not optional cleanup work.
