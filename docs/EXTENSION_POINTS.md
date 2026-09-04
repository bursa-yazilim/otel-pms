# QloApps Extension Points for Turkey Edition

## Status

**M0 initial map — source review complete, runtime validation pending**

This document identifies the safest current integration paths for Bursa Yazılım features. It does not authorize implementation against an unresolved-license component; licensing and architecture gates both apply.

Baseline commit:

`7318ae2c0056e1e0d4167424c942a28053ad1b08`

## Extension mechanisms confirmed from source

### Modules

QloApps uses PrestaShop-style modules extending `Module` or `PaymentModule`. Modules can:

- install/uninstall their own tables/configuration,
- register hooks,
- add admin tabs,
- provide front/back-office controllers,
- provide templates/CSS/JS,
- react to order/controller lifecycle events.

This is the preferred integration mechanism for Bursa-specific functionality.

### Hooks

Existing modules expose and consume hooks with methods named `hook...` and register hook lists during installation.

Observed examples include:

- `displayHeader`
- `actionFrontControllerSetMedia`
- `actionAdminControllerSetMedia`
- `displayPayment`
- `displayPaymentReturn`
- `actionValidateOrder`
- `displayBackOfficeHeader`
- `displayAdminListBefore`
- `addWebserviceResources`
- order-history and object lifecycle hooks in the hotel reservation module

The exact hook availability needed by each Bursa module must be confirmed before coding; missing events may justify a minimal documented core hook addition instead of direct business-logic edits.

### Webservice resources

`hotelreservationsystem` currently exposes hotel/PMS resources through `hookAddWebserviceResources()`, including:

- hotels,
- hotel room types,
- hotel amenities,
- hotel refund rules,
- hotel rooms,
- feature prices,
- advance payments,
- cart bookings,
- room bookings,
- hotel ARI (availability/rates/inventory) specific management.

These resources are useful for future integration boundaries, but external exposure/security must be reviewed before using them for KBS, mobile apps or external services.

### Overrides

The repository has an `override/` mechanism inherited from the platform. Overrides are preferred over direct core edits when a module/hook cannot satisfy the requirement, but they increase upstream conflict risk and must be documented.

### Themes/templates

Front-office branding and booking UX should use a Bursa-owned theme/template layer as far as the applicable theme licenses permit. Do not modify upstream theme files solely for branding when an inherited/custom theme can solve the requirement.

## Existing PMS model observations

### `HotelBookingDetail`

The current booking model already contains:

- order/cart/customer/room/hotel relationships,
- booking status,
- check-in and check-out timestamps,
- arrival/departure dates,
- room and hotel snapshots,
- adult/child occupancy,
- paid amount,
- cancellation/refund/back-order flags.

Status constants currently include:

- allotted,
- checked in,
- checked out.

### Guest Registration Card support

Current `develop` already contains a Guest Registration Card feature with configurable sections/fields for:

- guest details,
- travel information,
- booking information,
- identification documents,
- additional guests,
- billing/corporate details,
- payment/deposit,
- signature,
- property regulations,
- office use.

This is useful for Turkey Edition, but it does **not yet prove** that the data model is suitable for KBS or that every staying guest is persisted as a first-class record. M3 must verify persistence and normalize guest identity rather than stuffing Turkey-specific identity data into a printable card configuration.

## Planned Bursa modules / integration approach

### 1. Turkey Localization

Preferred implementation:

- language/localization data,
- configuration defaults,
- Bursa theme/template overrides,
- small module only where runtime behavior/defaults are required.

Avoid hard-coded Turkish strings in core files.

### 2. Turkey Guest Identity

Preferred implementation:

- Bursa-owned module with dedicated tables/models for staying guests when existing persistence is insufficient,
- relation to reservation/order/booking detail,
- back-office UI integration through hooks/controllers where possible,
- masking/permissions around TCKN/passport fields.

Do not overload `Customer` as the only staying guest; the reservation buyer and all occupants are different concepts.

### 3. Turkey KBS

Preferred implementation:

`bursaturkeykbs` (working name) module/service boundary.

Responsibilities:

- validate required staying-guest data,
- map internal guest data to official KBS format,
- submit through the officially supported mechanism,
- log request status/result safely,
- retry failed submissions,
- provide KBS operational dashboard.

Integration trigger candidates:

- explicit operator action at check-in,
- booking status/check-in lifecycle hook if reliable,
- a minimal new hook at the check-in transition if no safe existing event exists.

Do not call KBS from generic page rendering code.

### 4. Turkey Payment

Preferred implementation:

Create a new `PaymentModule`, following the platform payment contract rather than modifying existing Webkul payment modules.

The bundled Duitku module confirms a workable pattern using:

- `PaymentModule`,
- module-specific configuration,
- `displayPayment`,
- `displayPaymentReturn`,
- front/back-office media hooks,
- provider transaction storage,
- dedicated controllers/tables where necessary.

MVP should implement **one** provider (iyzico or PayTR), then abstract common behavior only when a second provider is justified.

### 5. Turkey SMS / Netgsm

Preferred implementation:

Bursa-owned module with provider interface.

Trigger candidates:

- reservation/order creation,
- reservation status changes,
- payment status events,
- scheduled pre-arrival reminders through cron/task mechanism.

Do not embed Netgsm calls directly in booking/order core classes.

### 6. WhatsApp

Post-MVP module using the same notification-event abstraction as SMS where practical. Provider/message costs and Meta template/consent rules remain external service concerns.

### 7. Bursa License Client

Preferred implementation:

Bursa-owned module/service that evaluates installation/license entitlements outside QloApps business entities.

Rules:

- no hard shutdown during active front-desk operations,
- grace period/read-only policy designed before enforcement,
- fail-safe behavior during Bursa License API outage,
- no customer PMS data sent to licensing service beyond strictly necessary installation/license metadata.

### 8. Channel Manager

Current repository contains `qlochannelmanagerconnector`, which reacts to `actionValidateOrder` and marks bookings originating from the channel-manager side.

Because both service/API terms and the bundled connector's source license require separate review, Turkey Edition should treat the channel manager as a replaceable external boundary. Do not tightly couple core PMS logic to this connector.

## Expected core-change pressure points

The following areas are likely to need careful review and may require new hooks if current ones are insufficient:

- atomic check-in/check-out transition events,
- saving multiple staying guests independently of the booking purchaser,
- after-payment/refund state transitions,
- reservation cancellation lifecycle,
- admin navigation/dashboard insertion,
- secure API/service callbacks.

Before editing a core class:

1. search for an existing hook,
2. search for module controller/service integration,
3. evaluate an override,
4. if still impossible, add the smallest stable hook/core change,
5. record it in `docs/CORE_PATCHES.md`,
6. add regression validation.

## M0 runtime validation still required

- [ ] Install a clean baseline and inspect enabled modules/hooks in a running instance.
- [ ] Confirm check-in/check-out event path and whether a reliable hook exists.
- [ ] Confirm order/reservation cancellation hooks.
- [ ] Confirm payment callback/controller conventions in a live install.
- [ ] Confirm cron/task manager behavior.
- [ ] Confirm override precedence and cache behavior.
- [ ] Confirm whether Guest Registration Card fields are persisted or generated from other data.
- [ ] Confirm API/webservice authentication and permissions.

After these tests this document should be updated from "initial map" to "validated extension map".
