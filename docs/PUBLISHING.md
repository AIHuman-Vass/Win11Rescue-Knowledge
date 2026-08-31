# Publishing signed Win11Rescue Knowledge Packs

## Rules

1. Knowledge packs are data only. Never place PowerShell, command lines, EXEs, DLLs, scripts, or arbitrary executable content in a pack.
2. Packs may only select `action_id` values defined by the Win11Rescue engine.
3. The private signing key must remain outside GitHub.
4. A pack is published only after schema validation, SHA-256 calculation, detached RSA signing, and verification.
5. `stable/latest.json` is updated last, after all pack files are present and verified.

## Recommended publish order

1. Create `stable/packs/<version>/knowledge.json`.
2. Validate against `schemas/knowledge.schema.json`.
3. Compute SHA-256 over the exact `knowledge.json` bytes.
4. Create detached signature `knowledge.sig` with the Win11Rescue Update Publisher private key.
5. Create `manifest.json` with URLs, SHA-256, and compatible engine version.
6. Verify signature using the public certificate.
7. Publish all three files.
8. Update `stable/latest.json` to point to the new manifest.

The same process applies to `preview/`.
