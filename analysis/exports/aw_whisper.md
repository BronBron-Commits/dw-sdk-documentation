# aw_whisper

## Signature
int aw_whisper(int target, char **message);

## Role
Sends a private (whisper) chat message to a specific target avatar or user.

## Preconditions
- aw_init must have been called
- SDK must be initialized
- A valid session/connection handle must exist
- Client must be inside a world or instance

## Behavior
- Verifies SDK initialized flag (TLS +0x7E0)
- Verifies presence of active session/connection handle (TLS +0x7E4)
- Checks internal string encoding mode (TLS +0x7E8)
- If internal encoding is Unicode:
  - Passes target and message directly to internal handler
- If internal encoding is non-Unicode:
  - Converts message string to wide-character format
  - Passes converted message to internal handler
- Delegates whisper send operation to an internal handler bound to the active connection

## State Effects
- No direct TLS field modification observed
- Triggers server-side private message delivery

## Return Values
- 0x1BC if SDK is not initialized
- 0x1BD if no session/connection handle is present
- Otherwise returns result from internal whisper handler

## Side Effects
- Initiates network activity related to private messaging
- Allocates temporary buffers for string conversion when required
- Delivery occurs asynchronously via events/callbacks

## Call Order Role
- Messaging function
- Used during active world participation
- Complements aw_say for private communication

## Notes
- Target parameter semantics are protocol-defined (avatar ID or user ID)
- Unicode and ANSI behavior mirrors aw_say
