---
name: synorb-manifests
description: Use when the user wants source-cited news, filings, podcasts or research from Synorb, asks which Streams or publishers Synorb covers, or asks about their Synorb plan or usage. Finds the right Streams first, then pulls Manifests with an explicit date window and cites the sources.
---

# Synorb Streams and Manifests

Synorb turns sources into Streams of Manifests. A Manifest is one source item with structured claims and a source URL. This skill covers the read tools. Saving a monitor is a different skill: `synorb-beacons`.

## Connection

The user signs in with Synorb OAuth when the plugin connects. Do not ask the user for a key or token. Do not call `synorb-get-demo-key` when the session is already signed in. That tool is only for a session that has no sign-in.

## Choose the tool

1. Account, plan or usage question: call `synorb-profile`. It does not use Manifest allowance.
2. "What do you cover?" or "do you have <publisher>?": call `synorb-stream-search`. It does not use Manifest allowance.
3. The topic is broad and the source is unclear: call `synorb-catalog`, then `synorb-details` with the Stream IDs you picked.
4. The user wants the content itself: call `synorb-manifests`.

Skip the discovery calls when the user already named the entity, ticker or source and the date window is clear. Call `synorb-manifests` directly.

## Rules for `synorb-manifests`

- Set an explicit date window every time: `days`, or `published_date_from` and `published_date_to`. Never rely on a default window.
- Pass every Synorb ID as a JSON string, never a number. The IDs have 17 digits and a number loses the last digits.
- `stream_ids`, `home_domains` and `source_channel_ids` are intersected, not united. When unsure, take `source_channel_ids` from `synorb-details` or `synorb-stream-search` instead of guessing.
- Start small: a `page_size` of 5 to 20. Ask before you page through more.
- Deduplicate by `manifest_id` when you combine pages or repeated calls.
- If the tool response has a usage or quota line, say it before the summary.

## Report the results

- Give each claim its source URL from the Manifest. Do not make up a citation from a title.
- Report the total count from the response `pagination`, not the number you happened to read.
- An empty result means nothing matched this scope and window. It does not prove the topic has no coverage. Say what you searched, then offer a wider window or a related Stream.
- `delivery_delta=true` reads a narrower population than an ordinary pull. A zero from it does not mean nothing matched. Repeat as an ordinary pull before you say that.
- If a call returns `401`, tell the user to reconnect Synorb in Plugins. Do not ask them to paste a key.
