vk-sync(-fork)
========
[![Latest version](https://img.shields.io/crates/v/vk-sync-fork.svg)](https://crates.io/crates/vk-sync-fork)
[![Documentation](https://docs.rs/vk-sync-fork/badge.svg)](https://docs.rs/vk-sync-fork)
[![](https://tokei.rs/b1/github/expenses/vk-sync-rs)](https://github.com/expenses/vk-sync-rs)

Simplified Vulkan synchronization logic, written in rust.

Forked off of the original [vk-sync](https://crates.io/crates/vk-sync) crate which is currently unmaintained.

- [Documentation](https://docs.rs/vk-sync-fork)
- [Changelog](https://github.com/expenses/vk-sync-rs/blob/main/CHANGES.md)

## Overview

In an effort to make Vulkan synchronization more accessible, this library provides an efficient simplification of core synchronization mechanisms such as pipeline barriers and events.

Rather than the complex maze of enums and bit flags in Vulkan - many combinations of which are invalid or nonsensical - this library collapses this to a much shorter list of ~40 distinct usage types, and a couple of options for handling image layouts.

Additionally, these usage types provide an easier mapping to other graphics APIs like DirectX 12.

Use of other synchronization mechanisms such as semaphores, fences and render passes are not addressed in this library at present.

## Bindings

There are a number of Vulkan ffi bindings available, and I do plan to support the most common bindings, but for now this library only implements support for [`ash`](https://crates.io/crates/ash). Please add other bindings you need via a pull-request; I would happily accept it.

## Expressiveness

Despite the fact that this library is fairly simple, it expresses 99% of what you'd actually ever want to do in practice. Adding the missing expressiveness would result in increased complexity which does not seem worth the trade-off. If you have any pattern you need express, please file an issue!

Here's a list of known things you cannot express:

* Execution only dependencies cannot be expressed. These are occasionally useful in conjunction with semaphores, or when trying to be clever with scheduling - but their usage is both limited and fairly tricky to get right anyway.

* Depth/Stencil Input Attachments can be read in a shader using either `ImageLayout::ShaderReadOnlyOptimal` or `ImageLayout::DepthStencilReadOnlyOptimal` - this library always uses `ImageLayout::DepthStencilReadOnlyOptimal`. It is possible (though highly unlikely) when aliasing images that this results in unnecessary transitions.

## Usage

Add this to your `Cargo.toml`:

```toml
[dependencies]
vk-sync = { package = "vk-sync-fork", version = "0.2.1" }
```

## License

Licensed under either of

 * Apache License, Version 2.0 ([LICENSE-APACHE](LICENSE-APACHE) or http://www.apache.org/licenses/LICENSE-2.0)
 * MIT license ([LICENSE-MIT](LICENSE-MIT) or http://opensource.org/licenses/MIT)

at your option.

## Credits

This library is heavily based on work by Tobias Hector (https://github.com/Tobski/simple_vulkan_synchronization) 

As mentioned above, this library was orignally developed by Graham Wihlidal (https://github.com/gwihlidal/vk-sync-rs)

## Contribution

Unless you explicitly state otherwise, any contribution intentionally submitted
for inclusion in this crate by you, as defined in the Apache-2.0 license, shall
be dual licensed as above, without any additional terms or conditions.

## Code of Conduct

Contribution to the vk-sync-fork crate is organized under the terms of the
Contributor Covenant, the maintainer of vk-sync, @gwihlidal, promises to
intervene to uphold that code of conduct.
