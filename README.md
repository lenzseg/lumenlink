# Lumenlink

![status](https://img.shields.io/badge/status-in_development-orange)

**Dual-MCU IoT light-control node:** STM32F446 (FreeRTOS) + ESP32-C6 (ESP-IDF) with custom serial communication protocol and web dashboard.

## Toolchains

| Tool | Version | Host |
|---|---|---|
| Arm GNU Toolchain (`arm-none-eabi`) | 15.3.rel2 | Linux x86_64 |

### Install the Arm GNU Toolchain

1. Download `arm-gnu-toolchain-15.3.rel2-x86_64-arm-none-eabi.tar.xz` from the
   [Arm GNU Toolchain downloads](https://developer.arm.com/downloads/-/arm-gnu-toolchain-downloads) page.
2. Extract it and create a version-independent symlink:

   ```bash
   sudo mkdir -p /opt/arm-gnu-toolchain
   sudo tar -xf arm-gnu-toolchain-15.3.rel2-x86_64-arm-none-eabi.tar.xz -C /opt/arm-gnu-toolchain
   sudo ln -sfn /opt/arm-gnu-toolchain/arm-gnu-toolchain-15.3.rel2-x86_64-arm-none-eabi \
                /opt/arm-gnu-toolchain/arm-none-eabi
   ```

   ```
   /opt/arm-gnu-toolchain/
   ├── arm-gnu-toolchain-15.3.rel2-x86_64-arm-none-eabi/
   └── arm-none-eabi -> arm-gnu-toolchain-15.3.rel2-x86_64-arm-none-eabi/
   ```

   > The symlink lets you upgrade the toolchain by repointing it, without editing PATH or build files.

3. Add it to your PATH (`~/.bashrc`) and verify:

   ```bash
   export PATH="/opt/arm-gnu-toolchain/arm-none-eabi/bin:$PATH"
   arm-none-eabi-gcc --version
   ```
