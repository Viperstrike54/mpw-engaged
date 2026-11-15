# MPW ENGAGED — CHECKPOINT 001
## Event Hub Development Wrap-Up

**Checkpoint Date:** November 14, 2026
**Project:** MPW ENGAGED
**Feature:** Event Hub — Shows & Match Cards
**Status:** Core functionality built and tested
**GitHub Repository:** Viperstrike54/mpw-engaged
**Live Event Hub:** https://viperstrike54.github.io/mpw-engaged/events.html

---

## 1. Purpose

The Event Hub manages official Mantra Pro Wrestling events and match cards. It allows administrators to create, edit, publish, and manage MPW shows while allowing public visitors to view published events.

This is an existing, working feature of MPW ENGAGED, not a proposed feature.

## 2. Technology

- HTML, CSS, and JavaScript
- GitHub Pages hosting
- Firebase Authentication
- Cloud Firestore
- Firebase JavaScript SDK 10.12.5

Firebase project ID: mpw-engaged

## 3. Completed Features

### Authentication
- Email/password sign-in
- Sign-out
- Administrator identification through users/{uid}
- Administrator access requires active == true and role == "admin"
- Public visitors can view published event cards without signing in

### Event Management
- Create event drafts
- Set event name, type, date, location, and description
- Edit existing event information
- Publish events
- Unpublish events and return them to drafts
- View published events
- View administrator drafts
- Open and close event details

### Match Card Management
- Add matches to events
- Enter match name, match type, and order
- Edit existing matches
- Delete individual matches
- Move matches up or down
- Save match order to Firestore
- Display main event at the top and opener at the bottom
- Display published match cards publicly

### Event Deletion
- Administrator event deletion controls exist
- Deletion requires confirmation and typing DELETE
- Empty-event deletion has been tested successfully

## 4. Testing Confirmed

The following were manually tested during development:

- Sign-in and sign-out
- Administrator controls
- Creating event drafts
- Editing event details and retaining changes
- Publishing an event
- Viewing a published event while signed out
- Adding, editing, and reordering matches
- Closing an open match card
- Deleting an empty event

Test Event 001 was deleted after testing.

Test Event 002 was used to test published match cards and match ordering, including matches involving Alexander Miles, Lee, Jared Balmer, Mr. Speed, Alex Reynolds, Aiden Miles, James Fatal, and Zach Moore.

These are test records, not confirmed MPW historical match results.

## 5. Firestore Structure

Primary collection:

events/{eventId}

Event fields used by the current page:
- title
- type
- date
- location
- description
- authorUid
- publicationStatus

Nested match collection:

events/{eventId}/matches/{matchId}

Match fields used by the current page:
- name
- type
- order
- createdAt

Other event subcollections referenced by security rules:
- private
- segments

User profiles:

users/{uid}

Relevant authorization fields:
- active
- role

## 6. Security Rules

Firestore rules are maintained separately from events.html.

The rules include:
- Administrator access to event management
- Contributor draft restrictions
- Public access to published events
- Public access to match cards belonging to published events
- Separate restrictions for private event information and show segments
- Default denial of other unspecified access

The current rules must be preserved in a separate checkpoint code snapshot.

## 7. Known Limitations

### Deleting Populated Events

Deletion of events containing matches has not been fully validated.

The current code deletes match documents in batches before checking whether private or segment records remain.

If deletion stops or fails after some match deletions, partial data loss is possible.

Future work should redesign and test this operation before treating populated-event deletion as safe.

### Match Booking

Current match booking uses text fields for match names and match types. Wrestlers are not yet linked through verified wrestler document IDs in this Event Hub.

### Match Results

The current Event Hub is primarily a booking and match-card management system. Automatic wrestler record updates, championship history updates, and match result processing are not yet verified features.

## 8. Relationship to Main Website

MPW ENGAGED already has a main website with navigation and an existing Roster system.

Roster V3, including Add Superstar, wrestler cards, and roster search/filter functionality, was built before this checkpoint.

Do not create a duplicate roster page without reviewing the existing implementation.

## 9. Future Development

Potential future work:
- Connect match participants to existing wrestler profiles
- Record official match results
- Link results to wrestler and division statistics
- Connect title matches to championship history
- Improve event deletion safety
- Support expanded match and segment management
- Import verified MPW historical events and results

These items are future development goals, not completed features.

## 10. Development Standards

For every major completed MPW ENGAGED milestone:

1. Build the feature.
2. Test the feature.
3. Confirm working behavior.
4. Save a development wrap-up.
5. Save separate snapshots of changed code and relevant rules.
6. Update the Project Master Log.
7. Continue to the next feature.

Preserve existing working functionality and avoid unnecessary rebuilding.

## 11. Checkpoint Status

Documentation: Prepared
Event Hub source: Supplied by user
Firestore rules: Supplied by user
GitHub checkpoint archive: In progress

**Next action:** Archive the source code and security rules alongside this document, then update the Project Master Log.

---

END OF CHECKPOINT 001 WRAP-UP
