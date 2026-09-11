# LooRadar Privacy & Security Baseline

## Privacy objective

LooRadar should minimize collection of personal information while still supporting useful community contributions and abuse prevention.

## Identity model

V1 uses Firebase Anonymous Authentication.

The app should not require users to provide:

- name
- email address
- phone number
- password
- social profile

Anonymous Firebase UIDs are internal identifiers and must not be displayed publicly.

## Location privacy

User location is sensitive and should be handled conservatively.

### Allowed use

Device location may be used to:

- center the map
- find nearby restrooms
- prefill a new restroom location when the user intentionally contributes one

### Prohibited by default

Do not persist:

- continuous location history
- historical searches tied to a user UID
- movement trails
- background location history

The public restroom coordinates submitted by a contributor are facility data, not user-location history.

## Permissions

Request foreground location only when needed.

Do not request background location in V1.

Explain the purpose in plain language before or alongside the OS permission prompt.

## Firebase security controls

Use:

- Firebase Authentication
- Firebase App Check
- restrictive Firestore Security Rules
- server timestamps
- validation of field types and ranges
- least-privilege Storage Rules when photos are introduced

Never rely exclusively on client-side validation.

## Contribution controls

Recommended controls:

- authenticated anonymous UID required for writes
- one rating per UID per restroom
- rate limits for submissions/reports/verifications
- duplicate-location checks
- maximum text lengths
- reject invalid latitude/longitude values
- constrain enum fields to known values
- moderation state for potentially abusive content

High-risk operations should move to trusted server-side code if Firestore Rules cannot enforce the business rule safely.

## Data minimization

Only collect information necessary for the restroom-finding service.

Avoid storing raw IP addresses, advertising identifiers, contacts, device fingerprints, or unrelated analytics unless a later requirement provides a clear justification and privacy review.

## Analytics

Analytics is not required for MVP functionality.

If analytics is introduced later:

- document it clearly
- minimize event parameters
- avoid precise-location analytics
- prefer aggregate product metrics
- review consent requirements by region

## Photos

Photos create additional privacy and moderation risks.

When introduced:

- discourage photographing people
- strip unnecessary metadata such as EXIF GPS where possible
- compress images before upload
- moderate before or shortly after publication
- support reporting/removal

## Public/private separation

Public UI must never expose:

- contributor UID
- moderation metadata
- internal abuse scores
- security logs

## Secrets

Do not commit unrestricted API keys or service-account credentials to GitHub.

Google Maps client keys must be platform-restricted using Android package/SHA restrictions and iOS bundle restrictions.

Backend credentials belong in managed secret/configuration systems.

## Privacy policy

A privacy policy is still required even without traditional accounts because the app processes location and uses third-party infrastructure.

The policy should describe at minimum:

- what data is processed
- use of location permission
- anonymous Firebase authentication
- community submissions
- Google/Firebase infrastructure
- retention and deletion approach
- user rights/contact process
- international data processing as applicable

## Default principle

When choosing between collecting data "because it may be useful later" and not collecting it, default to not collecting it.
