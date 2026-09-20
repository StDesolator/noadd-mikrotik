# Repository instructions

This fork packages noadd for MikroTik RouterOS Container on ARM64.

## RouterOS image contract

- Publish only `linux/arm64` for the `routeros-arm64` tag.
- The registry object must remain a Docker distribution v2 manifest with media
  type `application/vnd.docker.distribution.manifest.v2+json`.
- Keep provenance and SBOM attestations disabled because RouterOS must not see
  an OCI index in place of the image manifest.
- Keep producing a Docker archive (`type=docker`), not an OCI archive or a raw
  root-filesystem tarball, for `/container/add file=...` imports.
- Do not add secrets, real router exports, passwords, tokens, or private filter
  URLs to the repository or workflow artifacts.

## Router safety

- Never stop, remove, update, or overwrite an existing router container unless
  the user explicitly requests that exact action.
- Test new images in a separate container, veth, root directory, and data
  directory. Keep `start-on-boot=no` until testing is complete.
- Store container roots, temporary layers, and `/data` on external storage.
- Use explicit memory limits and measure both steady-state use and the filter
  rebuild peak before replacing an existing DNS service.

## Upstream maintenance

- Keep application changes suitable for upstream noadd; RouterOS-specific
  packaging belongs in the workflow and documentation where possible.
- Read `CLAUDE.md` and, before changing the filter engine, query pipeline, or
  storage layer, read `ARCHITECTURE.md` completely.
- Run the repository's formatting, lint, and test commands for source changes.
