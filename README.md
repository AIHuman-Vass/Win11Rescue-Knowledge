# Win11Rescue Knowledge

Public signed knowledge feed for Win11Rescue.

This repository contains versioned diagnostic rules, known-issue mappings, and repair recommendations consumed by Win11Rescue. It does **not** distribute executable repair code. Online packs may reference only predefined action IDs implemented and audited inside the Win11Rescue engine.

## Channels

- `stable/` - production knowledge feed.
- `preview/` - pre-release/testing feed.

## Trust model

Win11Rescue validates downloaded packs using SHA-256 plus a detached RSA signature pinned to the Win11Rescue Update Publisher public certificate embedded in the rescue image. The private signing key must never be stored in this repository.

If the online feed is unavailable or validation fails, Win11Rescue falls back to the newest valid cached pack and then to its built-in rules.

## Safety model

Knowledge packs are data-only. They can describe evidence, confidence, risk, Microsoft KB/build correlations, and a predefined `action_id`; they cannot contain PowerShell, command lines, DLLs, EXEs, or arbitrary executable instructions.

## Feed state

The repository is initialized but no signed production pack is published yet. `stable/latest.json` remains inactive until the first pack is signed with the Win11Rescue publisher key.
