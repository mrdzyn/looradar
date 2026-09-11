# LooRadar Data Model

## Design goals

- Support global restroom discovery.
- Support multiple restrooms at the same building coordinates.
- Keep reads inexpensive.
- Avoid storing unnecessary personal information.
- Support ratings, verification, reports, and future moderation.
- Keep the schema portable if spatial workloads later move to PostGIS.

## Collections

### `restrooms`

Suggested fields:

```text
id
name
latitude
longitude
geohash
countryCode
region
city
buildingName
buildingSection
floor
unitOrArea
landmark
directionsNote
accessType
feeAmount
feeCurrency
male
female
allGender
pwdAccessible
babyChanging
hasBidet
hasToiletPaper
hasSoap
hasHandDryer
averageRating
ratingCount
verificationCount
negativeVerificationCount
lastVerifiedAt
status
createdAt
createdByUid
updatedAt
```

### `ratings`

```text
id
restroomId
userUid
overall
cleanliness
supplies
accessibility
privacy
comment
createdAt
updatedAt
```

Recommended rule: one active rating per anonymous UID per restroom. Updating a rating replaces the user's prior rating rather than adding duplicates.

### `verifications`

```text
id
restroomId
userUid
result        // confirmed | not_found | temporarily_unavailable
createdAt
```

Use these records to maintain freshness indicators without exposing contributor identity publicly.

### `reports`

```text
id
restroomId
userUid
reason
notes
createdAt
status
resolvedAt
```

Suggested report reasons:

- duplicate
- permanently_closed
- wrong_location
- inaccurate_details
- inappropriate_content
- other

## Public versus private fields

Public facility data may include:

- restroom name
- coordinates
- building/floor directions
- amenities
- aggregate ratings
- verification freshness

Do not expose contributor UIDs in public responses or UI.

## Location representation

Coordinates represent the public facility, not the contributor's location history.

Store:

```text
latitude
longitude
geohash
```

For indoor facilities, additional text fields provide the useful final-leg directions.

## Rating aggregates

Do not compute aggregate ratings by loading every rating document whenever the marker/card is shown.

Store precomputed aggregate fields on the restroom document:

```text
averageRating
ratingCount
```

If category averages are useful later, add:

```text
averageCleanliness
averageSupplies
averageAccessibility
averagePrivacy
```

Updates should eventually be transaction-safe or performed in trusted server-side code.

## Duplicate detection

When submitting a new restroom:

1. Search for nearby restroom records within a small radius.
2. Compare building name, floor, and landmark metadata.
3. Warn the contributor if a likely duplicate exists.
4. Allow separate records for legitimate multiple restrooms in one building.

Do not automatically merge merely because coordinates are similar.

## Status values

Suggested restroom status values:

```text
active
unverified
flagged
temporarily_unavailable
removed
```

## Timestamps

Use server timestamps for mutation times where possible.

Store timestamps in UTC. Display dates/times in the user's locale.

## Future photo collection

When photos are introduced, use a separate metadata collection rather than embedding large arrays in restroom records.

Suggested fields:

```text
id
restroomId
storagePath
userUid
moderationStatus
createdAt
```

Photos should be compressed client-side and reviewed or automatically screened before becoming public.
