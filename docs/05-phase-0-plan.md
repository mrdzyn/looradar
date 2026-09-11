# LooRadar Phase 0 Plan

## Goal

Create the production-ready project foundation before feature implementation begins.

## Phase 0 deliverables

### Repository and Flutter foundation

- initialize Flutter application
- configure Android and iOS application identifiers
- establish folder structure
- enable strict analysis/linting
- add environment/config strategy
- add CI for format, analyze, and tests

### Firebase foundation

- create Firebase project environments as appropriate
- register Android and iOS apps
- configure Firebase Anonymous Authentication
- configure Cloud Firestore
- configure Firebase App Check
- create initial Firestore Security Rules
- create required composite indexes only as queries require them

Do not commit service-account secrets.

### Google Maps foundation

- enable Maps SDK for Android
- enable Maps SDK for iOS
- configure platform-restricted API keys
- add development map screen
- show current position only after permission is granted

Avoid enabling unrelated Google Maps Platform APIs during Phase 0.

### Domain model

Implement typed models for:

- restroom
- rating
- verification
- report

Implement enums rather than arbitrary strings for controlled values.

### Location foundation

- foreground location permission only
- permission-denied experience
- lat/lng value object
- geohash generation abstraction
- Haversine distance utility
- nearby-query repository interface
- map viewport query abstraction

### Data access architecture

UI must not call Firestore directly throughout the widget tree.

Use repository/service boundaries so that:

- Firestore can be tested/mocked
- geospatial strategy can be changed later
- PostGIS or another backend can eventually replace Firestore geo queries without rewriting UI

Suggested layering:

```text
presentation
  ↓
application/state
  ↓
domain
  ↓
data repositories
  ↓
Firebase / platform adapters
```

Do not over-engineer with excessive abstractions; preserve clear replacement boundaries around Firebase and GIS-specific operations.

### Security baseline

- authenticated anonymous UID required for writes
- public read access limited to fields/collections intended for public consumption
- validate latitude range -90..90
- validate longitude range -180..180
- validate controlled enums
- enforce text length limits
- block users from writing aggregate fields directly where practical
- App Check integration

### Testing foundation

Minimum Phase 0 tests:

- latitude/longitude validation
- Haversine distance calculation
- data model serialization/deserialization
- enum parsing
- repository contract test doubles
- permission-state logic where practical

## Non-goals

Phase 0 does not implement the complete product UX.

Specifically exclude:

- production add-restroom workflow
- ratings UI
- verification/reporting UI
- photos
- donation integration
- advanced moderation
- Places API
- routing APIs

## Definition of done

Phase 0 is complete when:

1. Flutter builds successfully for Android and iOS development targets.
2. CI passes format/analyze/tests.
3. Firebase initializes successfully.
4. Anonymous authentication produces a usable UID.
5. App Check is wired for development/testing and production strategy is documented.
6. Google Maps renders successfully.
7. Foreground location permission is handled correctly.
8. Current location can be represented on the map without persisting location history.
9. Domain/data repository boundaries are in place.
10. Geo utilities and core models have passing tests.
11. No secret credentials are committed to the repository.

## Next phase

Phase 1 should implement **Map Discovery**:

- nearby restroom query
- viewport querying
- marker rendering
- clustering
- restroom preview card
- nearby list
- initial filters
