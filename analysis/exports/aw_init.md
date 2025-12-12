# aw_init

## Signature
int aw_init(int mode);

## Inputs
- mode: integer value in range 0x41–0x65 (65–101)

## Outputs
- Returns 0 on success
- Returns 0x1C6 on invalid parameter

## Behavior
- Calls aw_term to clear any previous SDK state
- Initializes per-thread SDK context (TLS)
- Resets internal state blocks
- Seeds random number generation using time, PID, and rand
- Stores SDK mode/version
- Sets initialized flag

## State Effects
- Thread-local SDK context is created or reset
- Initialization timestamp recorded
- Session/world state cleared

## Side Effects
- No networking
- No file I/O
- No thread creation

## Call Order
- Must be called before any other SDK function
- Safe only once per thread unless aw_term is called

## Notes
- SDK uses TLS for all internal state
- Mode value may influence protocol or feature flags
