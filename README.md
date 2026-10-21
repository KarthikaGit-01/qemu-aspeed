# Running OpenBMC in QEMU on Ubuntu 24.04

This guide explains how to set up and run the `qemu-aspeed` emulator on Ubuntu 24.04 for the AST2600 EVB and AST2700 EVB platforms.

## Prerequisites

Tested on **Ubuntu 24.04**.

Install the required dependencies:

```bash
sudo apt update
sudo apt install libfdt1 libslirp0
```

## 1. Clone the Repository

Clone the `qemu-aspeed` repository and navigate to the project directory:

```bash
git clone https://github.com/KarthikaGit-01/qemu-aspeed
cd qemu-aspeed
```

Make the startup script executable if not run below command:

```bash
chmod +x qemu-aspeed.sh
```

## 2. Run QEMU for AST2600 EVB / CRB

Copy the `image-bmc`/`image-mtd` image from your OpenBMC build output directory into the current repository directory:

For EVB:

```bash
cp <openbmc_workspace>/<build_dir>/evb-ast2600/tmp/deploy/images/evb-ast2600/image-bmc .
```
For CRB:

```bash
cp <openbmc_workspace>/<build_dir>/<machine>/tmp/deploy/images/<machine>/image-mtd .
```

Start the AST2600 EVB emulator:

```bash
./qemu-aspeed.sh -i image-bmc -m 2600 -w 1234
```

## 3. Run QEMU for AST2700 EVB

Copy the AST2700 build output directory into the current repository directory:

```bash
cp -r <openbmc_workspace>/<build_dir>/ast2700-default/tmp/deploy/images/ast2700-default .
```

Start the AST2700 EVB emulator:

```bash
./qemu-aspeed.sh -i ast2700-default -m 2700 -w 1234
```

## Notes

- Replace `<openbmc_workspace>` and `<build_dir>` with the actual paths to your OpenBMC workspace and build directory.
- Ensure the required image files or directories exist before starting QEMU.
- The commands above use port `1234` for the `-w` option; refer to the emulator script's documentation for its exact purpose and configuration.
