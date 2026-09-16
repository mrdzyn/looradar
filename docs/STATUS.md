# LooRadar — Project Status

> Current-state coordination file for humans and AI agents. Keep this concise and update it at every meaningful handoff. Detailed history belongs in Git commits and PRs.

**Last updated:** 2026-09-16  
**Project:** LooRadar — global community-powered restroom finder  
**Repository:** `mrdzyn/looradar`  
**Overall stage:** Documentation / pre-implementation  
**Current phase:** Phase 0 — Foundation + UI shell/design system  
**Current branch:** `docs/phase-0-foundation`  
**Current PR:** #1 — `docs: establish LooRadar Phase 0 foundation`  
**Implementation status:** Not started

## Current objective

Finish and approve the product/technical foundation, merge the documentation baseline, then begin Phase 0 implementation from the repository source of truth.

## Locked decisions

- Product name: **LooRadar**.
- Global-first, mobile-first product.
- UI/UX-first delivery approach.
- Flutter for iOS and Android.
- Google Maps SDK for map visualization.
- Firebase Anonymous Authentication; no mandatory traditional login in V1.
- Cloud Firestore + geohashes for MVP GIS/nearby queries.
- Firebase App Check and restrictive Firestore rules are part of the security baseline.
- Foreground location only in V1.
- No persisted user movement/location history.
- External navigation handoff instead of building routing.
- Indoor location metadata (building/floor/wing/landmark/directions) is first-class.
- Photos deferred until after the core MVP workflow is proven.
- Optional donation/support model; no intrusive advertising planned for initial release.
- Low infrastructure cost and privacy-by-default are architectural constraints.

## Canonical references

Read these before implementation:

- `AGENTS.md` — multi-agent operating contract.
- `docs/README.md` — documentation index and current decisions.
- `docs/00-product-vision.md` — vision and product principles.
- `docs/01-architecture.md` — technical/GIS architecture and cost controls.
- `docs/02-data-model.md` — initial Firestore/domain model.
- `docs/03-privacy-security.md` — privacy and security baseline.
- `docs/04-mvp-scope.md` — MVP boundaries and acceptance criteria.
- `docs/05-phase-0-plan.md` — Phase 0 implementation plan and definition of done.
- `docs/06-ui-ux-reference.md` — UX rules and validation gates.
- `docs/assets/looradar-mobile-ux-reference.png` — **canonical visual reference** for user-facing implementation.

## Completed

- Initial product vision documented.
- Flutter/Firebase/Google Maps architecture documented.
- GIS strategy defined using lat/lng + geohash candidate queries + exact distance filtering.
- Indoor-location metadata strategy defined.
- Initial Firestore/domain data model documented.
- Anonymous identity and location-privacy model documented.
- MVP scope and phased roadmap documented.
- Phase 0 plan and definition of done documented.
- UI/UX-first approach documented.
- Canonical mobile mockup checked into `docs/assets/`.
- Multi-agent orchestration contract added as `AGENTS.md`.
- Cross-agent status/handoff ledger added as this file.

## Active work

Documentation PR #1 is the active milestone. No application implementation should begin until the documentation baseline is reviewed/merged unless the human owner explicitly changes that sequence.

## Phase 0 implementation scope

Once documentation is merged, Phase 0 should establish:

- Flutter application scaffold and identifiers;
- clean project/layer structure;
- strict analysis/linting and CI;
- environment/config strategy with no committed secrets;
- Firebase initialization;
- anonymous authentication;
- Firestore foundation and initial security rules;
- Firebase App Check strategy/integration;
- Google Maps Android/iOS setup with restricted keys;
- foreground location permission flow;
- UI shell/design tokens/components guided by the canonical mockup;
- typed core domain models and enums;
- lat/lng value object, geohash abstraction, and Haversine utility;
- repository/service boundaries around Firebase/GIS/platform dependencies;
- foundational unit tests.

See `docs/05-phase-0-plan.md` for the authoritative definition of done.

## Not started / later phases

**Phase 1 — Map Discovery:** nearby and viewport queries, restroom markers, clustering, preview cards/list, initial filters.

**Phase 2 — Add Restroom:** adjustable map pin, location/building/floor/landmark metadata, amenities/access fields, duplicate warning, anonymous submission.

**Phase 3 — Ratings + Verification + Reporting:** community quality signals and freshness workflows.

**Phase 4 — Moderation / Trust / Production Hardening:** abuse controls, stronger aggregation/moderation workflows, production readiness.

**Phase 5 — Growth features:** photos, broader/open-data integrations, and other validated enhancements.

## Current blockers / human actions

- Review/audit PR #1.
- Merge PR #1 after approval.
- Google/Firebase project configuration and production credentials will require owner-controlled setup during Phase 0.
- Google Maps API keys must be platform-restricted and must not be committed as unrestricted secrets.

## Validation status

This milestone is documentation-only. Application build/test validation has **not started**.

- Product/architecture docs — PRESENT
- Privacy/security baseline — PRESENT
- MVP/Phase 0 scope — PRESENT
- Canonical PNG UI reference — PRESENT
- `AGENTS.md` — PRESENT
- `docs/STATUS.md` — PRESENT
- Flutter format/analyze/test — NOT RUN; app not scaffolded yet
- Android build — NOT RUN; app not scaffolded yet
- iOS build — NOT RUN; app not scaffolded yet
- Firebase runtime validation — NOT RUN; Phase 0 implementation pending
- Google Maps runtime validation — NOT RUN; Phase 0 implementation pending

## Next recommended action

**Audit PR #1 as the final documentation baseline.** Verify consistency across product scope, architecture, privacy/security, Phase 0 requirements, canonical UX reference, `AGENTS.md`, and this status file. Resolve any findings, then merge PR #1.

After merge, create a dedicated Phase 0 implementation branch/PR and instruct the implementation agent to read `AGENTS.md` + `docs/STATUS.md` before touching code.

## Handoff template

Every implementation agent should update the current sections above and leave a compact handoff in this format:

```text
Task:
Branch:
Commit:
PR:

Implemented:
- ...

Validation:
- ... — PASS | FAIL | NOT RUN

Docs updated:
- ...

Blockers / risks:
- ...

Next recommended action:
- ...
```

Do not preserve stale completed-task detail here merely for history. Keep this file useful to the **next agent**.