# bsp-iot-gate-imx8plus

Carrier board support for the CompuLab **IOT-GATE-iMX8PLUS** industrial IoT
gateway, built on the **UCM-iMX8M-Plus** SOM.

This is a *carrier* BSP extension: the buildable Avocado MACHINE is the SOM
(`ucm-imx8m-plus`), and this extension adapts a SOM image to the gateway
carrier. It does two things:

1. **Selects the gateway device tree.** The SOM MACHINE builds the
   `iot-gate-imx8plus` DTBs into the boot partition. On merge, this extension
   points the U-Boot env `devicetree_file` at `iot-gate-imx8plus.dtb`
   (via `fw_setenv`), so the gateway boots its own DT without a separate
   MACHINE.
2. **Brings up the gateway peripherals.** Cellular modem (MHI:
   `mhinet`/`mhitty`/`mhiuci` + ModemManager), GPS (`gpsd`), and CAN
   (`flexcan`).

## Using this extension

In your project `avocado.yaml`:

```yaml
default_target: ucm-imx8m-plus

extensions:
  avocado-bsp-iot-gate-imx8plus:
    source:
      type: package
      version: "*"

runtimes:
  production:
    extensions:
      - avocado-bsp-iot-gate-imx8plus
```

Then:

```sh
avocado install
avocado build
```

## Board features

- NXP i.MX 8M Plus SoC (UCM-iMX8M-Plus SOM)
- Cellular modem (MHI / ModemManager)
- GNSS / GPS (gpsd)
- CAN bus
- Optional M.2 TPM (`iot-gate-imx8plus-m2tpm.dtb`)
