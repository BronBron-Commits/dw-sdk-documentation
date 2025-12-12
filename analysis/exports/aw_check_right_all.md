# aw_check_right_all

## Signature
bool aw_check_right_all(char *right);

## Role
Checks whether a specific right is granted across all applicable targets.

## Preconditions
- SDK instance list must be initialized
- At least one instance must exist

## Behavior
- Verifies at least one instance exists
- Uses the first available instance for rights evaluation
- Checks internal string encoding mode (TLS +0x7E8)
- If Unicode mode:
  - Passes right string directly to internal rights checker
- If non-Unicode mode:
  - Converts right string to wide-character format
  - Passes converted string to internal rights checker

## State Effects
- None
- Pure query against internal rights system

## Return Values
- 1 if the specified right is granted for all applicable contexts
- 0 otherwise

## Side Effects
- No networking
- No persistent state changes

## Call Order Role
- Authority / permission query function
- Used to verify global permissions before performing operations

## Notes
- Semantics of "all" are defined internally by the SDK
- Often used for admin or elevated rights checks
