# Thunderbolt 3 Unblocker

This project provides a kernel extension that unblocks unsupported Thunderbolt
3 peripherals (such as the Razer Core) on macOS.

This accomplishes the same goal as [KhaosT's TB3 Enabler][tb3-enabler], which
works by patching IOThunderboltFamily on disk. This kernel extension performs
the patch in memory and on-the-fly.

[tb3-enabler]: https://github.com/KhaosT/tb3-enabler

Note there is likely a reason why IOThunderboltFamily considers a peripheral
unsupported in the first place. Use at your own peril.

This kernel extension was last tested against macOS High Sierra 10.13.4. Please
check for [open issues][issues] before using on newer versions.

[issues]: https://github.com/rgov/Thunderbolt3Unblocker/issues

## Installation

To prepare your development environment, please run

    git submodule update --init --recursive
    brew install cmake

Build the project with Xcode. Make sure to change code signing settings as
appropriate.

It is recommended that you keep as many System Integrity Protection features on
as possible; use `csrutil enable --without kext`. If you are not using code
signing, you can additionally set `nvram boot-arg="kext-dev-mode=1"`.

Load the kernel extension with:

    sudo chown -R root:wheel Thunderbolt3Unblocker.kext
    sudo kextload Thunderbolt3Unblocker.kext


## `xnu_override`

This project also implements a simple, reusable in-memory kernel patching
library. The author has released it under a permissive license in the hopes
that it will be useful.
