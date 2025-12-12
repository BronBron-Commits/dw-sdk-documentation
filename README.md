# DeltaWorlds SDK – Behavioral Documentation

This repository documents the **observable behavior** of the DeltaWorlds / ActiveWorlds-style SDK as derived from static analysis, decompilation, and runtime reasoning.

It is not an SDK implementation, not a binary mirror, and not protocol source code.

It is a **behavioral specification**.

---

## Purpose

The goal of this project is to define a **single source of truth** for how the SDK behaves so that:

- A compatible client or viewer can be implemented
- A Unity-based frontend can be built
- Tooling, bots, or automation can interoperate correctly
- Multiple clients can coexist in the same server instance

Compatibility is defined by **behavior**, not by internal structure.

---

## What This Repository Is

- A reverse-engineered behavioral contract
- A reference for correct call ordering
- A description of state transitions and invariants
- Documentation of permissions, events, and side effects
- Suitable for reimplementation or API bridging

---

## What This Repository Is Not

- Not an SDK distribution
- Not decompiled source code
- Not a protocol byte-level specification
- Not a server implementation

---

## Repository Structure

analysis/exports  
Documentation for individual SDK API calls, including:
- Preconditions
- State effects
- Return values
- Side effects
- Call-order role

analysis/state  
High-level behavioral models, including:
- SDK state machine
- Thread-local state assumptions
- Event and callback flow

analysis/protocol  
Observed protocol-level behavior and sequencing  
(No raw packet dumps)

analysis/ghidra  
Notes related to reverse engineering methodology and tooling

---

## Core Concepts

### Thread-Local Runtime
- Each thread has its own SDK context
- The SDK is not reentrant
- One active connection or instance per thread

### Explicit Event Pump
- The SDK does not use background threads
- Progress only occurs when aw_wait is called
- Callers must drive the event loop manually

### Server Authority
- The server is the single source of truth
- Client calls stage intent, not state
- Permissions gate all mutations

### Observable Compatibility
- Correct return codes matter
- Silent failures are part of the contract
- Timing and ordering are significant

---

## Minimal Correct Client Flow

1. aw_init  
2. Configure callbacks and events  
3. aw_login  
4. aw_enter or aw_join  
5. Main loop:
   - aw_wait
   - process callbacks  
6. aw_exit  
7. aw_term  

Skipping or reordering steps results in undefined behavior.

---

## Getting the Official SDK

The official DeltaWorlds SDK is publicly available from the vendor.

You can obtain the SDK, headers, and documentation directly from:

https://www.deltaworlds.com/

This repository does not redistribute the SDK or any of its components.

All behavioral documentation here is intended to be used alongside the official SDK, or as a reference for building compatible tooling, viewers, or alternative clients that interoperate correctly.

Always ensure you are using the SDK in accordance with the applicable license terms provided by DeltaWorlds.

---

## Legal and Ethical Notes

This repository contains:
- No proprietary binaries
- No decompiled source listings
- No protocol byte dumps

All content is derived from:
- Behavioral observation
- Public interfaces
- Independent analysis

Use of this documentation must comply with the applicable SDK and server license terms.

---

## Status

This repository currently documents:
- Full client lifecycle
- Event and callback system
- Object and avatar behavior
- Messaging and interaction
- Permission and rights model
- World metadata and configuration
- Complete SDK state machine

This is sufficient to build a **fully compatible client or viewer**.

---

## Next Possible Extensions

- Formal state diagrams per subsystem
- Unity reference implementation notes
- ABI compatibility headers
- Automated conformance test cases
