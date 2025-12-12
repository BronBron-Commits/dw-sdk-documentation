# aw_world_attributes_change

## Signature
int aw_world_attributes_change(void);

## Role
Commits or packages pending world attribute changes for transmission or application.

## Preconditions
- aw_init must have been called
- SDK must be initialized
- A valid session/connection handle must exist
- One or more world attributes must have been staged or modified

## Behavior
- Verifies SDK initialized flag (TLS +0x7E0)
- Verifies presence of active session/connection handle (TLS +0x7E4)
- Delegates attribute change packaging to an internal configuration packager
- Prepares modified world attributes for application or network transmission

## State Effects
- Flushes or commits pending world attribute changes
- No direct TLS modification observed

## Return Values
- 0x1BC if SDK is not initialized
- 0x1BD if no session/connection handle is present
- Otherwise returns result from internal configuration packager

## Side Effects
- Initiates network activity related to world attribute updates
- May trigger world attribute change events or callbacks

## Call Order Role
- World configuration finalization function
- Must be called after one or more aw_world_attribute_set calls
- Completes the world metadata update cycle

## Notes
- Acts as a commit/apply step for batched world attribute changes
- Ordering relative to aw_world_attribute_set is significant
