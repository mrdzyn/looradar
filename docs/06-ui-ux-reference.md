# LooRadar UI/UX Reference

## Purpose

LooRadar is a **UI/UX-first project**. The core mobile experience should be designed and validated before backend scope expands.

The checked-in visual reference is:

![LooRadar mobile UX reference](assets/looradar-mobile-ux-reference.svg)

This mockup is the initial visual and interaction reference for implementation. It is not a pixel-perfect final design specification, but the build should preserve the user journey, hierarchy, and interaction model unless a documented UX decision replaces it.

## Core UX principles

1. **Map first.** The primary screen is the map with nearby restroom markers.
2. **Immediate utility.** Users should be able to find nearby restrooms without creating an account.
3. **Low-friction contribution.** Adding a restroom should require only the minimum useful information.
4. **Useful quality signals.** Ratings, amenities, access type, and recent verification should help users choose quickly.
5. **Indoor context matters.** Building, floor, wing, landmark, and indoor directions are first-class fields because GPS alone is insufficient in malls, airports, stations, and large buildings.
6. **Privacy by default.** Foreground location is used to serve the immediate request and is not retained as user movement history.
7. **Global language.** Use terms such as restroom/toilet in product UI while allowing localized terminology later.
8. **Accessibility.** Touch targets, contrast, text scaling, labels, and screen-reader support should be considered from the first implemented screens.

## Primary screen sequence

### 1. Splash / value proposition

Goal: communicate what LooRadar does before requesting location permission.

Key content:

- LooRadar brand
- short value proposition
- nearby restroom discovery
- ratings/amenities
- community contribution
- no account required
- primary Get Started action

### 2. Map / discovery

Goal: get the user to a suitable restroom with minimal interaction.

Key components:

- Google Map
- current-position indicator
- restroom pins
- search field placeholder for future/local search capability
- map controls
- nearest-restroom card/list
- marker clustering at dense zoom levels
- quick visible signals such as rating, distance, access/open status where available

The map remains useful even when no restroom records are currently nearby.

### 3. Restroom details

Goal: answer "Is this restroom suitable for me?"

Show:

- place/building name
- floor/wing/landmark
- overall rating and count
- access/open status where reliably known
- amenities
- accessibility information
- indoor directions
- recent verification status
- Directions action
- Rate action
- Verify / Report actions

Photos are represented conceptually in the mockup but remain post-MVP unless scope is explicitly changed.

### 4. Add restroom

Goal: make a useful contribution fast.

Flow:

1. start from current location or selected map point;
2. show adjustable pin;
3. enter place/building;
4. optionally enter floor/wing;
5. optionally enter landmark/indoor directions;
6. select useful amenities/access attributes;
7. run duplicate warning;
8. submit using anonymous Firebase identity.

Do not require personal profile information.

### 5. Filters

Initial filters should remain concise and task-oriented. Examples:

- open now only when trustworthy opening-hours data exists
- free
- paid
- customer only
- accessible
- baby changing
- male
- female
- all gender
- bidet
- tissue
- soap
- recently verified

Avoid turning the first release into a long preference form.

## Additional flows to design before implementation

The generated design exploration also establishes the direction for these supporting screens:

- ratings and reviews
- external navigation choices
- menu/settings/support
- onboarding/location-permission explanation
- successful contribution confirmation

These should be implemented only when their phase is reached, but their interaction model should remain consistent with the map-first experience.

## UI design direction

Current visual direction:

- clean, modern mobile utility
- light/default theme first
- blue as the primary action/map-marker color
- white and neutral surfaces
- green for positive/open/verified status
- amber for ratings/warnings where appropriate
- rounded cards and controls
- strong whitespace and uncluttered maps
- bottom sheets/cards preferred for map-context actions

Dark mode can be added after the core UX is stable unless platform defaults make it inexpensive to support earlier.

## Design-system expectations

Before large-scale feature implementation, establish reusable tokens/components for:

- spacing
- typography
- corner radius
- elevation
- semantic status colors
- buttons
- chips/filter pills
- form fields
- map markers and clusters
- restroom cards
- amenity icons/rows
- empty/error/loading states

Do not scatter arbitrary visual constants across individual screens.

## UX validation gates

A phase that changes the user-facing workflow should include:

1. updated screen/wireframe or explicit confirmation that the existing reference still applies;
2. implementation matching the intended hierarchy and interaction path;
3. empty, loading, error, permission-denied, and offline/degraded states where applicable;
4. accessibility review;
5. screenshot/manual QA on representative Android and iOS device sizes.

## Source-of-truth rule

When implementation and this reference disagree:

- documented product requirements and security/privacy rules take precedence;
- intentional UX changes must be documented in the same pull request;
- accidental drift from the mockup is a defect, not a silent design decision.

The intent is to keep LooRadar **UI/UX first, architecture-supported**, rather than allowing backend implementation convenience to dictate the user experience.
