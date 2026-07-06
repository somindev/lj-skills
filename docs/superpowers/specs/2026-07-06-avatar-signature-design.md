# Avatar and Signature Replacement

## Goal

Replace the generated cards' displayed identity with Li Jun's assets and signature on the `my-version` branch.

## Changes

- Make `ljg-card` use `assets/logo-lj.png`.
- Make `ljg-library` and `ljg-map` use their local `assets/lj-portrait.png` files as character references.
- Change rendered signatures from `李继刚` to `李珺`.
- Update instructions and verification checklists that directly describe these avatar and signature outputs.

## Boundaries

- Keep plugin author metadata, repository URLs, installation commands, original author credits, and historical notes unchanged.
- Keep the new asset filenames distinct from the upstream filenames.
- Avoid unrelated formatting, refactoring, and content changes.

## Verification

- Search active templates and generation scripts for old avatar references and rendered `李继刚` signatures.
- Confirm all new asset paths exist.
- Render representative `ljg-card`, `ljg-library`, and `ljg-map` outputs when the local tooling permits.
- Review the final diff and confirm every changed line supports the avatar or signature replacement.
