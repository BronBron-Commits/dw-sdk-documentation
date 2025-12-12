# aw_instance_wait

## Signature
int aw_instance_wait(int instance);

## Role
Waits for a specific instance to become ready and switches the active instance context when available.

## Preconditions
- aw_init must have been called
- SDK must be initialized
- Instance enumeration must be available

## Behavior
- Verifies SDK initialized flag (TLS +0x7E0)
- Saves the current active instance handle
- Searches internal instance list for the requested instance value
- If instance is not found, restores previous instance and returns error
- If found:
  - Temporarily sets the active instance to the requested value
  - Checks readiness state of the instance
  - If not ready, waits using internal wait/dispatch logic
  - Processes internal queue/events related to instance readiness
- Restores or updates active instance handle depending on outcome

## State Effects
- Temporarily modifies TLS active instance field (TLS +0x7E4)
- May release and reacquire instance-related resources
- Restores previous instance handle on failure

## Return Values
- 0 on success (instance ready and active)
- 0x1BC if SDK is not initialized
- 0x1BD if instance is invalid or cannot be waited on

## Side Effects
- May block while waiting for instance readiness
- Processes internal event or message queues
- Releases and reacquires instance-related resources
- No direct networking initiated at this level

## Call Order Role
- Synchronization / transition function
- Used after aw_instance_set to ensure instance readiness
- Required before performing instance-dependent operations

## Notes
- Function is stateful and may temporarily alter active instance context
- Designed to safely revert state on failure
- Internally enforces instance validity and readiness
