# LooRadar Documentation

This folder is the source of truth for the initial LooRadar product and technical foundation.

## Documents

1. [`00-product-vision.md`](00-product-vision.md) — product problem, value proposition, global positioning, and product principles.
2. [`01-architecture.md`](01-architecture.md) — Flutter/Firebase/Google Maps architecture, GIS strategy, cost controls, and scaling path.
3. [`02-data-model.md`](02-data-model.md) — Firestore collections, restroom fields, ratings, verification, reports, and duplicate-handling guidance.
4. [`03-privacy-security.md`](03-privacy-security.md) — anonymous identity model, location privacy, App Check, security rules, data minimization, and secret handling.
5. [`04-mvp-scope.md`](04-mvp-scope.md) — MVP features, exclusions, primary screens, acceptance criteria, and initial success measures.
6. [`05-phase-0-plan.md`](05-phase-0-plan.md) — concrete Phase 0 implementation requirements and definition of done.
7. [`06-ui-ux-reference.md`](06-ui-ux-reference.md) — UI/UX-first build rules, screen flows, design direction, validation gates, and the checked-in mobile mockup.

## Visual reference

![LooRadar mobile UX reference](assets/looradar-mobile-ux-reference.svg)

The visual reference is part of the project source of truth. User-facing implementation should follow its hierarchy and interaction model unless an intentional design change is documented in the same pull request.

## Current architectural decisions

- Product name: **LooRadar**
- Global-first mobile application
- UI/UX-first delivery approach
- Flutter for iOS and Android
- Google Maps SDK for map visualization
- Firebase Anonymous Authentication rather than mandatory user registration
- Firestore + geohash strategy for MVP GIS queries
- No stored user movement/location history
- No background location permission in V1
- External navigation handoff instead of implementing routing
- Photos deferred until after the core map/contribution workflow is proven
- Optional donation/support model rather than mandatory monetization in V1

## Development sequence

```text
Phase 0 — Foundation + UI shell/design system
   ↓
Phase 1 — Map Discovery
   ↓
Phase 2 — Add Restroom
   ↓
Phase 3 — Ratings + Verification + Reporting
   ↓
Phase 4 — Moderation / Trust / Production Hardening
   ↓
Phase 5 — Photos, broader data integrations, growth features
```

Any implementation decision that materially changes these documents or the approved interaction model should update the documentation in the same pull request.
