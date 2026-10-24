# Lumenlink

![status](https://img.shields.io/badge/status-in_development-orange)

**Dual-MCU IoT light-control node:** STM32F446 (FreeRTOS) + ESP32-C6 (ESP-IDF) with custom serial communication protocol and web dashboard.

## Toolchains

| Tool | Version | Host |
|---|---|---|
| Arm GNU Toolchain (`arm-none-eabi`) | 15.3.rel2 | Linux x86_64 |
| ESP-IDF (installed with EIM) | v6.1 | Linux x86_64 |

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

### Install ESP-IDF

ESP-IDF and its tools (RISC-V compiler, CMake, Ninja, Python environment) are installed with
**EIM**, the ESP-IDF Installation Manager. On Linux, install the EIM CLI through `apt`.

1. Install the prerequisites (build tools, USB access, and the libraries used by the optional QEMU emulator):

   ```bash
   sudo apt update
   sudo apt install -y \
     git wget flex bison gperf ccache dfu-util \
     libffi-dev libssl-dev libusb-1.0-0 \
     python3 python3-pip python3-venv \
     libgcrypt20 libglib2.0-0 libpixman-1-0 libsdl2-2.0-0 libslirp0
   ```

2. Add the Espressif APT repository and install the EIM CLI:

   ```bash
   echo "deb [trusted=yes] https://dl.espressif.com/dl/eim/apt/ stable main" | sudo tee /etc/apt/sources.list.d/espressif.list
   sudo apt update
   sudo apt install -y eim-cli
   ```

   > `[trusted=yes]` skips APT signature checks for this repository. Only use it with the official Espressif URL.

3. Install the pinned ESP-IDF version for the ESP32-C6 (files go to `~/.espressif/`):

   ```bash
   eim install -t esp32c6 -i v6.1
   ```

4. Allow your user to access the board's serial port, then log out and back in:

   ```bash
   sudo usermod -aG dialout $USER
   ```

5. Activate ESP-IDF in each new terminal and verify:

   ```bash
   source ~/.espressif/tools/activate_idf_v6.1.sh
   idf.py --version
   ```

   > Activate it per terminal instead of adding it to `~/.bashrc`; it loads its own Python environment and tool paths.
