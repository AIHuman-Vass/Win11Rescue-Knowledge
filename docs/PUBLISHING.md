# Publishing signed Win11Rescue Knowledge Packs

## Safety rules

1. Knowledge packs are data only. Never place PowerShell, command lines, EXEs, DLLs, scripts, or arbitrary executable content in a pack.
2. Packs may only select `repairAction` values implemented and whitelisted by the Win11Rescue engine.
3. The private signing key must remain outside GitHub. Never upload a PFX/private key.
4. Every active pack must pass SHA-256 verification and detached RSA/SHA-256 signature verification against the public certificate pinned in Win11Rescue.
5. `stable/latest.json` is updated last, only after the pack and signature are present.

## Repository layout

```
stable/
  latest.json
  packs/
    <version>/
      knowledge-pack.json
      knowledge-pack.sig
preview/
  latest.json
  packs/
    <version>/
      knowledge-pack.json
      knowledge-pack.sig
```

## Publisher workflow

On the authorized publisher Windows PC, run `tools/SIGN-STABLE-PACK.cmd` from Win11Rescue v0.2.3 or later. The publisher tool uses the private key in `Cert:\CurrentUser\My`, creates the exact JSON bytes, computes SHA-256, creates the detached RSA/SHA-256 signature and generates the matching `latest.json`.

Publish in this order:

1. `<channel>/packs/<version>/knowledge-pack.json`
2. `<channel>/packs/<version>/knowledge-pack.sig`
3. `<channel>/latest.json` **last**

Win11Rescue rejects a pack if its signature, SHA-256, publisher thumbprint, rule structure, risk values, operators, or repair-action IDs do not pass local validation.

The pinned official publisher SHA-1 thumbprint is `075685CEB4D796E69E8275486E444EB62826EBC5`.
