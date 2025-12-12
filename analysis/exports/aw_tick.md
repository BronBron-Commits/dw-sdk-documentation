# aw_tick

## Summary
aw_tick is the core time source and heartbeat of the DeltaWorlds SDK.
It does not mutate world, instance, or object state.
It computes and returns a monotonically increasing timestamp derived from system time and per-thread baseline offsets.

This function anchors polling, waiting, and deferred event processing.

## Signature
undefined8 aw_tick(void)

Returns a 64-bit timestamp value.

## Preconditions
- None
- Does not require an active world
- Does not require initialization state flags
- Always callable

## Behavior
- Reads current system time via GetSystemTime
- Manually computes a millisecond-resolution timestamp
- Accounts for:
  - Leap years
  - Month lengths
  - Day, hour, minute, second, millisecond components
- Subtracts a thread-local baseline stored at:
  - TLS + 0x800 (low)
  - TLS + 0x804 (high)
- Returns a 64-bit value composed from:
  - Low 32 bits: milliseconds since baseline
  - High 32 bits: overflow / carry accumulation

## State Effects
- None
- Pure computation

## Side Effects
- Reads system clock
- Reads thread-local storage
- No allocation
- No networking

## Call Order Role
- Primary SDK clock
- Used by aw_wait and event pump loops
- Drives time-based state progression

## Notes
This function is foundational to the SDK’s state machine.
Rather than timers or callbacks, the SDK advances by repeatedly sampling aw_tick
and comparing against stored temporal thresholds.

In effect:
- Time is not pushed
- Time is polled
- Progress emerges from repeated evaluation

This design enables deterministic behavior, offline simulation,
and single-threaded control over the entire client lifecycle.
