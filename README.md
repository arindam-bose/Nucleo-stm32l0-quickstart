```
     __  __  __    __  ______
    /\ \/ / /\ "-./  \/\  == \\
    \ \  _"-\ \ \-./\ \ \  __<
     \ \_\ \_\ \_\ \ \_\ \_____\\
      \/_/\/_/\/_/  \/_/\/_____/    STM32L053R8 Quickstart
```
June 9, 2021

# `STM32L053R8-quickstart-`

> A template for building applications for ARM Cortex-M0+ microcontrollers especially for Nucleo-L0 board

## Dependencies

To build embedded programs using this template you'll need:

- Rust 1.31, 1.30-beta, nightly-2018-09-13 or a newer toolchain. e.g. `rustup
  default beta`

- The `cargo generate` subcommand. [Installation
  instructions](https://github.com/ashleygwilliams/cargo-generate#installation).

- `rust-std` components (pre-compiled `core` crate) for the ARM Cortex-M
  targets. Run:

``` console
$ rustup target add thumbv6m-none-eabi thumbv7m-none-eabi thumbv7em-none-eabi thumbv7em-none-eabihf
```

## Using this template

**NOTE**: This is the very short version that only covers building programs. For
the long version, which additionally covers flashing, running and debugging
programs, check [the embedded Rust book][book].

[book]: https://rust-embedded.github.io/book

0. Before we begin you need to identify some characteristics of the target
  device as these will be used to configure the project and modify it accordingly:


1. Instantiate the template.

``` console
$ cargo generate --git https://github.com/KMB-Telematics/stm32l0-quickstart
 Project Name: app
 Creating project called `app`...
 Done! New project created /tmp/app

$ cd app
```

2. Set a default compilation target. There are four options as mentioned at the
   bottom of `.cargo/config`. For the STM32L053R8T6, which has a Cortex-M0+
   core, we'll pick the `thumbv6m-none-eabihf` target.

``` console
$ tail -n6 .cargo/config
```

``` toml
[build]
# Pick ONE of these compilation targets
target = "thumbv6m-none-eabi"    # Cortex-M0 and Cortex-M0+
# target = "thumbv7m-none-eabi"    # Cortex-M3
# target = "thumbv7em-none-eabi"   # Cortex-M4 and Cortex-M7 (no FPU)
# target = "thumbv7em-none-eabihf" # Cortex-M4F and Cortex-M7F (with FPU)
```

3. Enter the memory region information into the `memory.x` file.

``` console
$ cat memory.x
/* Linker script for the STM32F303VCT6 */
MEMORY
{
  /* NOTE 1 K = 1 KiBi = 1024 bytes */
  FLASH : ORIGIN = 0x08000000, LENGTH = 64K  /* STM32L053R8*/
  RAM : ORIGIN = 0x20000000, LENGTH = 8K     /* STM32L053R8*/
}
```

4. Build the template application or one of the examples.

``` console
$ cargo build
```