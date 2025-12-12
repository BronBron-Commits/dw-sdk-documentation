DeltaWorlds SDK – Behavioral Documentation

This site documents the observable behavior of the DeltaWorlds / ActiveWorlds-style SDK as derived from static analysis, decompilation, and runtime reasoning.

It is a behavioral specification, not an SDK implementation.

---

Purpose

This documentation defines a single source of truth for SDK behavior so that compatible clients, viewers, and tooling can be implemented correctly.

Compatibility is defined by behavior, not by internal structure.

---

Core Concepts

Thread-Local Runtime  
Each thread owns its own SDK context. The SDK is not reentrant.

Explicit Event Pump  
The SDK makes no forward progress unless aw_wait is called.

Server Authority  
The server is the single source of truth. Client calls stage intent only.

---

Minimal Correct Client Flow

1. aw_init  
2. Configure callbacks and events  
3. aw_login  
4. aw_enter or aw_join  
5. Main loop:
   - aw_wait
   - process callbacks and events  
6. aw_exit  
7. aw_term

---

Getting the Official SDK

The official SDK is available from:

https://www.deltaworlds.com/

This project does not redistribute SDK binaries or headers.
