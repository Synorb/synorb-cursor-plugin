---
name: synorb-beacons
description: Use when the user wants to watch a company, topic or source over time with Synorb, or asks about their saved Beacons. Lists Beacons first, drafts a proposal, and saves or archives a Beacon only after the user says yes to that exact Beacon.
---

# Synorb Beacons

A Beacon is a saved monitor: a scope of Streams, sources and filters that you pull again later. Synorb does not run schedules and does not push updates. The user's own agent pulls a saved Beacon when it chooses to.

## Reads need no permission

- `synorb-beacons` lists the saved Beacons, including the starter Beacons with the tag `starter`. Call it before you propose anything, so you do not suggest a Beacon the user already has.
- `synorb-configure-beacon` drafts a proposal from an intent. It only previews and writes nothing.

When you know the user's role, projects or interests, you may propose one to three Beacons with a one-line reason each. A proposal is not a save.

## Writes need a clear yes

- `synorb-save-beacon` writes to the user's account. Call it only after the user has said yes to that proposal, or has asked for a saved or recurring monitor. Pass the proposal that `synorb-configure-beacon` returned.
- `synorb-archive-beacon` removes a Beacon from use. Call it only after the user says yes to that specific `beacon_id`. This includes starter Beacons.
- Never save or archive on your own initiative, and never to make room. If a save fails because the plan has reached its Beacon limit, tell the user and ask which Beacon to archive.
- Pass every Synorb ID as a JSON string, never a number.

## Run a saved Beacon

Call `synorb-manifests` with `beacon_id` and an explicit lookback, either `days` or `lookback_hours`. A Beacon does not set its own run window. Deduplicate by `manifest_id` across runs.

The save response includes a `dashboard_url`. It opens only for signed-in members of the owning organization. Share it with the user when they ask where to see the Beacon.
