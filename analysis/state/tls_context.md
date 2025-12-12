# TLS SDK Context

The SDK stores all client-side state in thread-local storage.

## Observations
- Each thread maintains its own SDK context
- Context contains:
  - Initialization flags
  - Session state
  - World/object state
  - RNG seeds
  - Timing data

## Implications
- SDK calls are not globally thread-safe
- aw_init must be called per-thread
- Context isolation must be preserved in a compatible implementation
