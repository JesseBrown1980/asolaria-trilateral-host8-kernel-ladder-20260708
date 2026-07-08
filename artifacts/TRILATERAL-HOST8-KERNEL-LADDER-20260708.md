# Trilateral Host8 Kernel Ladder Spec

Status: DESIGN / E=0 / no code port. Created 2026-07-08T10:01:03Z.

## Decision

Map first, code later. Acer-side direction is accepted: OMNIMETS and OMNISCHEDULER are old Node/V8 semantics that must be ported into Host8 stub-room receiver slots, not replaced by a heavier new router.

## Root Cause

Old OMNIMETS uses in-memory counters plus NDJSON at `~/.asolaria-workers/omnimets-events.ndjson`. If the Node process is cold, the route is stale even though disk telemetry exists. Host8 rooms are preallocated disk-backed receiver slots: route a tuple/string into the room, index by 8-byte handle, answer from HBP/HBI without spinning a Node service.

## Port Contract

- Keep the six-body lanes: muscular, skeletal, nervous, circulatory, endocrine, digestive, cross.
- Keep events: DISPATCH, DEFER, HALT, PROMOTE, ERROR.
- Keep `omnimets-scheduler-crypto-policy.v1`: fresh metrics, PID-bound scheduler, idempotency key, stale-lock halt, bounded backoff, crypto capsule metadata.
- Bind to existing `ROOMSTUB` rows and Host8 route semantics.
- Derive `host_handle8 = sha256(id|room_stub)[..16]`.
- Store hot path as HBP/HBI, `json=0`; JSON/NDJSON remains cold compatibility until parity retires it.
- `process_launch=0`, `auto_fire_allowed=false`, E=0 until operator/cosign gate.

## Trilateral Ladder

Axis 0: seat hardware and driver gap.
Axis 1: Host8 room/service surface.
Axis 2: time/proof row.

The 2D maps are projections from this 3D structure. Each seat emits its local layer; the other two attack-verify sidecars, row counts, handle derivation, and driver gaps.

## Seat State

ACER: operator-observed Acer Nitro AN515-52 with Intel RST/VMD 8086:282A; kernel driver gap is VMD/RST storage.

LIRIS: measured old OMNIMETS data and Host8 stub-room files on disk; live OMNIMETS route is stale/no-cache; hardware-specific kernel driver remains ungrounded here.

RELIC: onboarding candidate, branch `relic`; Windows 11 Home, 3.89 GB RAM, 110.89 GB C:, OpenCode/API/tools observed in Relic report; hardware driver gap ungrounded here.

## Evidence Boundary

Fabric health and OMNIMETS routes are stale/cache-bound here. Loop pending shows 20 E=0 held envelopes. Council query for this publish returned action_confirmed=false due all_bases_unavailable. This packet is a GitHub coordination artifact, not a live fabric decision.
