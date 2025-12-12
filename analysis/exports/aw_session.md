# aw_session

## Signature
int aw_session(void);

## Role
Query function that returns the current session identifier or state derived from the active connection.

## Preconditions
- aw_init must have been called
- SDK must be initialized
- A valid session/connection handle must exist

## Behavior
- Reads the thread-local SDK context
- Verifies initialized flag
- Verifies presence of a non-null session/connection handle (TLS +0x7E4)
- Delegates to an internal handler to retrieve the session value
- Returns 0 if preconditions are not met

## State Effects
- None
- Pure read of existing state via internal handler

## Return Value
- Returns session value from internal handler on success
- Returns 0 if SDK is not initialized or no session/connection handle exists

## Side Effects
- None
- No networking at this level
- No memory allocation

## Call Order Role
- Query / inspection function
- Safe to call after connection setup
- Used to check session readiness or identity

## Notes
- Session value is derived, not stored directly in TLS
- Depends on the same handle used by aw_login and aw_address
