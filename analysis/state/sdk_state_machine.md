# SDK State Machine

This document describes the behavioral state machine of the DeltaWorlds / ActiveWorlds-style SDK as derived from reverse engineering and runtime analysis.

This is a behavioral contract, not an implementation description.

---

## High-Level SDK State Diagram

State flow:

[*] -> Uninitialized

Uninitialized -> Initialized : aw_init  
Initialized -> Uninitialized : aw_term  

Initialized -> NoConnection : init complete  
NoConnection -> Connected : aw_connection_set / aw_login  
Connected -> NoConnection : aw_exit / aw_term  

Connected -> InWorld : aw_enter / aw_join  
InWorld -> Connected : aw_exit  

InWorld -> InWorld : aw_wait  
InWorld -> InWorld : events and callbacks dispatched  

InWorld -> InWorld : object, avatar, chat APIs  
InWorld -> InWorld : world attribute staging  

InWorld -> WorldConfigPending : aw_world_attribute_set  
WorldConfigPending -> InWorld : aw_world_attributes_change  

Connected -> Connected : aw_wait  
Connected -> Connected : limited events and callbacks  

NoConnection -> NoConnection : aw_wait (no-op)

Uninitialized -> [*]

---

## State Definitions

### Uninitialized
- SDK has not been initialized
- All API calls fail
- Entry state

### Initialized
- Thread-local SDK context allocated
- Callback and event tables zeroed
- No connection active

### NoConnection
- SDK initialized
- No active session or instance
- Only configuration and query calls are valid

### Connected
- Valid session/connection handle present
- Not yet inside a world
- Limited event processing available

### InWorld
- Client has entered a world or instance
- Full API surface available
- Objects, avatars, chat, camera, and world attributes are valid

### WorldConfigPending
- One or more world attributes staged
- Changes not yet committed
- Must be followed by aw_world_attributes_change

---

## Core Invariants

### Initialization Gate
All meaningful SDK calls require:
- aw_init has been called
- TLS initialized flag is set

Failure results in return code:
- 0x1BC

---

### Connection Gate
World, object, avatar, and messaging calls require:
- Active session or connection handle

Failure results in return code:
- 0x1BD

---

### Event Pump Rule (Critical)

The SDK does not use background threads.

Progress only occurs when:
- aw_wait is called

This includes:
- Event dispatch
- Callback invocation
- Join and enter completion
- State synchronization

Clients must call aw_wait regularly, typically once per frame.

---

## Callback and Event Dispatch Sub-State

InWorld internal flow:

Idle  
Idle -> Processing : aw_wait  
Processing -> Idle : no events  
Processing -> CallbackDispatch : event received  
CallbackDispatch -> Idle : handler returns  

---

## Implications for Client Implementations

- The SDK maps directly onto a game-loop architecture
- aw_wait should be called from the main update loop
- No assumptions should be made about asynchronous progress
- Permissions must be checked explicitly before mutating state
- Observable behavior, not internal structure, defines compatibility

---

## Summary

This state machine represents the minimum correct behavioral model required to build:
- A compliant client
- A Unity-based viewer
- A bot or automation client
- An API-compatible reimplementation

Any implementation that respects this model will coexist correctly with the original SDK.
