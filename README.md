# Win11Rescue Knowledge

Public signed knowledge feed for Win11Rescue.

This repository contains versioned diagnostic rules, known-issue mappings, and repair recommendations consumed by Win11Rescue. It does **not** distribute executable repair code. Online packs may reference only predefined `repairAction` IDs implemented and audited inside the Win11Rescue engine.

## Channels

- `stable/` - production knowledge feed.
- `preview/` - pre-release/testing feed.

## Trust model

Win11Rescue validates downloaded packs using SHA-256 plus a detached RSA/SHA-256 signature pinned to the Win11Rescue Update Publisher public certificate embedded in the rescue image. The private signing key is never stored in this repository.

Official publisher SHA-1 thumbprint: `075685CEB4D796E69E8275486E444EB62826EBC5`.

The public certificate and metadata are available under `certificates/` for transparency; Win11Rescue trusts the copy pinned inside its boot image, not a certificate downloaded from the repository.

If the online feed is unavailable or validation fails, Win11Rescue falls back to the newest valid cached pack and then to its built-in rules.

## Safety model

Knowledge packs are data-only. They can describe diagnostic evidence, confidence, risk, Windows build/KB correlations and a predefined `repairAction`; they cannot contain PowerShell, command lines, DLLs, EXEs, or arbitrary executable instructions. The client also applies a local action whitelist and rule-structure validation after signature verification.

## Feed state

The repository is initialized but no signed production pack is published yet. `stable/latest.json` remains `active: false` until the first pack is signed with the Win11Rescue publisher private key.
