# [Documentation](https://docs.rs/libdaisy)

## libdaisy
Hardware Abstraction Layer implementation for Daisy boards.

## Requirements

### A Flashing Utility
* [Electro-smith web programmer](https://electro-smith.github.io/Programmer/)

OR

* [dfu-util](http://dfu-util.sourceforge.net/)

OR

* [Probe.rs](https://probe.rs/)

This requires a debug probe of some sort (e.g. ST link) and allows for fast debugging messages via RTT.

cargo embed --features log-rtt --example passthru

## Using this template

Because we write code on our local computer and it has a different architecture than the ARM Cortex-M, we have to cross-compile. Using `rustup` ([an installer for Rust](https://rustup.rs/)), we grab the appropriate target because the Seed falls under Cortex-M4F and M7F with hardware floating point (ARMv7E-M architecture) we use:

```
rustup target add thumbv7em-none-eabihf
```

We also install `cargo-binutils` in order to use Cargo subcommands to invoke the LLVM tools shipped with the Rust toolchain:

```
cargo install cargo-binutils
rustup component add llvm-tools-preview
```

Next, install `cargo-generate` so that you can easily grab a template for your project:

```
cargo install cargo-generate
```

Then, you will use `cargo-generate` to grab a template:

```
cargo generate --git https://github.com/githubusername/mytemplate.git
```

Run the base template via:

```
cargo objcopy --release -- -O binary template.bin
```

Then (if you're using `dfu-util`):

```
dfu-util -a 0 -s 0x08000000:leave -D template.bin
```

## Build Other Examples

```
cargo objcopy --example blinky --release -- -O binary blinky.bin
```

```
cargo objcopy --example passthru --release -- -O binary passthru.bin
```


## Minimum supported Rust version

The Minimum Supported Rust Version (MSRV) at the moment is 1.51.0.

## Demos

[Looper](https://github.com/mtthw-meyer/daisy-looper) - Basic one button looper.
