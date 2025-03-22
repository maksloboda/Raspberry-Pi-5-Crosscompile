# Cross compiling Rust from linux to Raspberry Pi 5

This repository is mostly made so I dont forget all the little quirks I had to look for.

Based on [this guide](https://github.com/robamu-org/rpi-rs-crosscompile), but it does not work as-is for Raspberry 5.

I assume you already have rust installed and that you are using Raspberry OS lite.

1. Download toolchain from [here](https://developer.arm.com/downloads/-/arm-gnu-toolchain-downloads), you are looking for "AArch64 GNU/Linux target" most likely its going to be "arm-gnu-toolchain-[VERSION]-x86_64-aarch64-none-linux-gnu.tar.xz". I compiled with "arm-gnu-toolchain-14.2.rel1-x86_64-aarch64-none-linux-gnu.tar.xz" on my x86 64bit laptop.
2. Unarchive the files somewhere and add them to your path like this
`export PATH="[PATH TO YOUR FOLDER]/arm-gnu-toolchain-[VERSION]-x86_64-aarch64-none-linux-gnu/bin:$PATH"`
3. Run `rustup target add aarch64-unknown-linux-gnu`
4. Specify linker for our target `export CARGO_TARGET_AARCH64_UNKNOWN_LINUX_GNU_LINKER=aarch64-none-linux-gnu-gcc`. In theory you can specify this in cargo.toml but in my testing it gets ignored for some reason.
5. Compile `cargo build --target aarch64-unknown-linux-gnu`
6. Transfer to your Raspberry Pi 5 and execute.
