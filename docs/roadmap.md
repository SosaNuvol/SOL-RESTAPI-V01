# Review and implementation roadmap

## Decisions before coding

Recommended defaults are proposals, not confirmed business rules.

| Decision | Proposed default |
| --- | --- |
| Languages | C# backend; TypeScript web/mobile; T-SQL database |
| Lead conversion | Create/reuse customer at accepted order; mark paying status from posted non-reversed payment allocations |
| Sales credit | Copy lead reps to customer; freeze order attribution separately; decide equal/custom splits and commission basis |
| Installer pay | Accrue approved hourly/fixed/piece compensation per work order; record actual payout allocations separately |
| Warranty | Versioned policy and coverage per system/component; assess each service case; business supplies duration and exclusions |
| Multiple homes | One customer, many properties; each property can have several installed systems |
| Mobile delivery | Two React Native apps with shared libraries; confirm iOS/Android requirements and distribution |
| Offline needs | Assigned-job records, topology, downloaded photos, and queued field edits; confirm maximum offline period |
| GoHighLevel | Begin with inbound lead/contact/opportunity sync; confirm location IDs, pipeline rules, available authentication and permissions |
| Hosting | Evaluate existing SQL Server vs Azure SQL, identity provider, private file storage and backup requirements |
| Initial ERP scope | Operational sales/field service/costing; integrate with existing accounting rather than build a general ledger at launch |

Also establish expected staff/job counts, existing data imports, product catalog and units, accounting/payment systems, tax/invoicing needs, property ownership transfers, photo retention, and who approves topology and payouts.

## Phases and acceptance gates

1. **Confirm design.** Approve stack and business rules, sample one real installation and repair, define permissions and CRM mappings. Deliver finalized schema/API contracts and screen designs.
2. **CRM and sales foundation.** Identity, party/customer/property records, many-to-many representative attribution, GoHighLevel import, accepted orders and payment records. Gate: repeated CRM events produce one result; conversion preserves reps; one customer can acquire another home without duplicate accounts.
3. **Installation operations.** Catalog, systems, installer assignments, material/labor costing, photos and topology revisions. Gate: two installers can share a job; three houses remain distinct; every splitter/booster can be found through description/photo; historical job cost survives product price changes.
4. **Service and installer mobile.** Cases, warranty assessment, repair evidence, offline cache, command queue and upload recovery. Gate: offline repair synchronizes once; stale topology cannot overwrite a published change; missing photo uploads block documented completion.
5. **Sales mobile and compensation.** Lead/quote workflow, order attribution, accruals, payout allocations and reports. Gate: shared reps do not double-count revenue; partial payments/refunds and partial installer payouts remain traceable.
6. **Pilot and production readiness.** Real field trials, permission checks, CRM rate-limit/retry handling, monitoring, backup restore, mobile distribution and staff training. Gate: restore SQL and evidence together; confirm access isolation and field usability on real devices.

Sequence can change after business review. No schedule estimate is justified until team size, integration access, and offline scope are known.

## High-value scenarios to validate

- Two leads for an existing person convert to the same customer without losing either lead's rep history.
- A customer with three properties receives separate installations, warranty coverage, and service history.
- Multiple reps split one sale; replacing the account's assigned rep does not rewrite earlier commissions.
- Multiple installers earn different amounts; payout reports distinguish accrued, approved, paid, and remaining balances.
- Replacing a splitter records old and new assets, locations, costs, photos, and the approved topology revision.
- Duplicate payment callbacks and webhook retries do not duplicate money or leads.
- Two offline installers edit one system; the second submission creates a reviewable conflict.
- An installer cannot download an unassigned customer's photos by guessing an attachment identifier.

## Proposed repository layout after approval

```text
apps/erp-web/                 React + TypeScript
apps/installer-mobile/        React Native + TypeScript
apps/sales-mobile/            React Native + TypeScript
src/Solasta.Api/              ASP.NET Core API
src/Solasta.Application/      Use cases and authorization
src/Solasta.Domain/           Business rules and entities
src/Solasta.Infrastructure/   SQL Server, storage, CRM adapters
src/Solasta.Worker/           Inbox/outbox and scheduled sync
packages/api-client/         Generated TypeScript client
packages/mobile-shared/      Mobile components and sync helpers
tests/                       Business/integration/mobile scenarios
docs/                        Design and decisions
```

Create these projects only after stack review. This folder currently contains the design documents only.
