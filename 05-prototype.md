# Prototype and design specifications

Input: 04-solution-design.md. Open prototype.html for a working browser-only reservation simulator; index.html embeds a financial calculator.

## Scope
A demonstrator, not a deployed marketplace. Select one of three clearly fictional lots, reserve, confirm collection, expire a lot or reset. State persists in localStorage on the same browser origin. Reservation prevents duplicate reservation in this browser only; server concurrency, authentication, payments and real food transfers are not implemented. Status and receipt are announced in a polite live region. No personal data is requested.

## Specification
Responsive breakpoint 760 px; minimum control height 44 px; system sans font with optional Google Inter; visible focus outline; reduced-motion support. Shared CSS and SVG favicon. Lot fields: id, shop alias, kilograms, price per kilogram, pickup cutoff, state, actual kilograms. States: available → reserved → collected; available/reserved → expired. Collected is terminal. Actual weight must be >0 and ≤ listed weight. Reset restores fixtures. Expiry is explicitly simulated; production must use server timestamps in Europe/Moscow and enforce cutoffs on every write.

Production API proposal: POST /lots; POST /lots/{id}/reservation with idempotency key and atomic available-state update; POST /reservations/{id}/pickup with expiring code, actualKg and timestamp. RBAC separates shop, buyer and operator; audit trail includes cancellations and rejection reasons. Encrypt transport; minimise retained data; define retention and deletion with local counsel.

## Physical kit
Concept only: washable reusable 100×70 mm lot-label sleeve, printable QR/lot identifier and food-contact-compliant crate sourced after supplier validation. Do not attach non-compliant materials directly to food. Retail scale accuracy target ±50 g verified daily; this is a proposed requirement, not a tested hardware claim.

## Acceptance checks
Three fixture lots render; reserve changes only available lot; collect accepts valid actual weight and generates receipt; invalid weight blocks collection; expiry removes collection actions; reset restores three available lots; reload preserves state. Keyboard navigation, mobile stacking and no horizontal overflow are required. Browser checks and limitations recorded in README.md.

Landing calculator: recovered retail sales = kg/day × days/month × ₽/kg. Fee = ₽1,500 + 5% of sales. Retailer proceeds = sales − fee, excluding tax, labour and normal-sales displacement. Negative values remain visible. Model inputs are illustrative and do not forecast actual savings.
