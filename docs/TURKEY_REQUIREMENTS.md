# Turkey Edition Requirements

## Target customer

Initial commercial target:

- 8–30 room boutique hotels,
- apart hotels,
- pensions,
- bungalow properties,
- small accommodation businesses.

Large full-service hotels are not the initial target because they commonly require deeper integrations such as restaurant POS, PBX, door locks, spa, agency accounting and complex finance workflows.

## Product positioning

Turkey-focused PMS and booking platform combining front desk operations with local compliance and local providers.

Core value proposition:

`Reservation + PMS + KBS + direct booking + payment + SMS/WhatsApp + OTA connectivity`

## P0 — Saleable MVP

### Professional Turkish localization

- Complete user-facing Turkish terminology review.
- Turkish locale/date/time conventions.
- TRY/TL display and currency defaults.
- Turkey timezone defaults.
- Turkish phone formatting/validation where appropriate.
- Turkish province/district address structure.

### Guest identity model

The reservation owner and staying guests must be separate concepts.

Each staying guest should support, as applicable:

- name,
- surname,
- TCKN,
- passport/document number,
- nationality,
- birth date,
- gender if legally/operationally required,
- phone,
- email,
- address,
- check-in/check-out relationship.

A single reservation must support multiple staying guests.

### KBS integration

- Isolated Turkey KBS module/service.
- Required-field validation before submission.
- submission status,
- error/result logging,
- retry workflow,
- operator/audit information.

Important: do not design implementation around an assumed public REST API. The current official integration method and authorization process must be validated before implementation.

### Payment

Initial provider: choose one of iyzico or PayTR for MVP.

Support:

- full payment,
- deposit/advance payment,
- remaining balance,
- paid/partially paid/unpaid status,
- provider transaction reference,
- refund/cancellation model where supported.

Do not store raw card data.

### SMS

Initial provider: Netgsm.

Events:

- reservation created,
- reservation confirmed,
- cancellation,
- pre-arrival reminder,
- payment reminder,
- optional check-out/post-stay message.

Provider code must be abstracted so additional Turkish providers can be added later.

### Direct booking engine

- Fully Turkish booking flow.
- Mobile-first usability.
- arrival/departure search,
- guest/room selection,
- room/rate selection,
- optional extras,
- guest details,
- deposit/full payment,
- confirmation.

Provide an easy way for an existing hotel website to link/embed the booking flow.

## P1 — After saleable MVP

- WhatsApp Business integration.
- Channel manager connection.
- e-Fatura/e-Arşiv or accounting integration bridge.
- advanced owner reports.
- PWA/mobile operational views.
- richer hotel website/booking widgets.
- automated pre-arrival and post-stay workflows.

## Channel manager principle

Do not build a new Booking.com/Airbnb/Expedia channel manager in the first product phase. OTA partner/API access, mapping, rate/availability restrictions and certification can become a separate product-scale effort.

Use an approved existing provider initially, with the integration boundary kept replaceable.

## Accounting and e-invoice principle

Do not block MVP on full Turkish accounting functionality. The first version may export required billing data or integrate with one selected provider. Full accounting is out of scope for initial release.

## Operational UX

Primary daily screens should prioritize:

- arrivals today,
- departures today,
- currently staying guests,
- room calendar,
- available/occupied rooms,
- reservations,
- check-in/check-out,
- housekeeping,
- outstanding balances,
- KBS status.

Do not delete upstream functions to achieve simplicity. Hide or de-emphasize advanced functions through navigation/configuration/permissions.

## Initial reporting requirements

Minimum owner reports:

- daily revenue,
- monthly revenue,
- occupancy,
- average room rate,
- reservation source,
- unpaid/outstanding balance,
- cancellations,
- future 30-day reservation view.

## KVKK and privacy requirements

Because the system processes identity and stay data:

- collect only data with a defined operational/legal purpose,
- control access by role,
- log access/actions where appropriate,
- mask identifiers where full display is unnecessary,
- establish data retention/deletion rules,
- document processor/controller responsibilities with customers,
- never commit real guest data or credentials to Git.

Legal text and retention rules must be reviewed for the actual commercial deployment model before launch.
