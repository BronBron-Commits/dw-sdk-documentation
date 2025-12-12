# Ghidra Analysis Notes

This directory contains notes specific to Ghidra analysis.

## Conventions
- Decompiled code is treated as evidence, not ground truth
- Assembly listings override decompiler output if discrepancies appear
- Offsets are recorded relative to TLS base where applicable

## Tools Used
- Ghidra (PE loader, decompiler, function graphs)
- SDK headers imported as C for type accuracy
