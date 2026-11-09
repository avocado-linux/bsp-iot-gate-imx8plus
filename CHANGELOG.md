# Changelog

All notable changes to avocado-bsp-iot-gate-imx8plus are documented in this file.
The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [0.1.0]

### Added
- Initial release: carrier board support for the CompuLab IOT-GATE-iMX8PLUS,
  built on the UCM-iMX8M-Plus SOM (target `ucm-imx8m-plus`). Selects the
  `iot-gate-imx8plus` device tree at boot and brings up the gateway CAN bus.
- CI via the shared `avocado-linux/actions` reusable workflows: PR build check
  (`test.yml`) and tag-driven package + publish to the Avocado feed
  (`release.yml`), both against `ucm-imx8m-plus` on the 2024 and 2026 next
  feeds.
- `avocado-devicetree` in the package set: `on_merge` runs its
  `avocado-devicetree-apply`, and without it the extension merge failed.

### Removed
- The `mhinet`, `mhitty` and `mhiuci` autoloads: neither feed builds those
  modules. The in-tree MHI drivers bind by PCI modalias.
