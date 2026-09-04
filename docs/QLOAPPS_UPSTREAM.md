# QloApps Upstream Strategy

## Purpose

This document defines how Bursa Yazılım will consume upstream QloApps changes without mixing upstream development with product-specific work.

## Repositories

- Upstream: `Qloapps/QloApps`
- Fork: `bursa-yazilim/otel-pms`

## Branch ownership

### `develop`

Upstream tracking branch.

Rules:

- Keep it as close as possible to `Qloapps/QloApps:develop`.
- Do not add Turkey Edition product features directly to it.
- Do not perform branding work directly on it.
- Do not remove upstream features from it.
- Use it to inspect and import upstream fixes/features.

### `main`

Commercial product integration branch.

Contains Bursa Yazılım features, modules, overrides, themes, documentation and approved upstream updates.

### Working branches

Use short-lived branches from `main`:

- `feature/<name>`
- `fix/<name>`
- `chore/<name>`

Merge to `main` via PR after review and tests.

## Initial upstream baseline

Fork baseline:

`7318ae2c0056e1e0d4167424c942a28053ad1b08`

At M0 start, the fork's `develop` branch matches this upstream commit.

The separately downloadable QloApps 1.7.0 ZIP is not used as a baseline and must not be copied over the repository.

## Upstream update workflow

When QloApps publishes new commits:

1. Sync fork `develop` from upstream `develop`.
2. Review upstream changelog/commit range.
3. Classify changes:
   - security,
   - bug fix,
   - PHP/runtime compatibility,
   - database/schema,
   - PMS/reservation behavior,
   - API/webservice,
   - UI/theme,
   - module behavior,
   - license/third-party dependency.
4. Compare against `main`.
5. Apply upstream changes to a dedicated integration branch from `main`.
6. Resolve conflicts with documented reasoning.
7. Run install/upgrade and functional smoke tests.
8. Merge only after the product build is stable.

## Core modification register

Any modification under upstream core paths that cannot be implemented as a module/override/theme must be recorded in a future `docs/CORE_PATCHES.md` file before the relevant milestone is closed.

Each record must include:

- file path,
- product commit,
- reason,
- expected upstream conflict,
- related module/feature,
- regression test or manual validation steps.

## Versioning

QloApps' internal version string is not sufficient to identify the actual product baseline because current `develop` may retain the same displayed install version while containing substantially newer code.

Otel PMS releases must therefore use Bursa Yazılım-owned version identifiers in addition to recording the QloApps baseline commit.

Suggested format:

- product version: `0.x.y` until commercial 1.0
- release tag: `otel-pms-v0.x.y`
- metadata: upstream QloApps commit SHA

## Upstream compatibility principle

We will not freeze permanently on the initial fork commit. Upstream updates are valuable, but they are never merged blindly into the commercial branch.
