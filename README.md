# `"optimize_for_size"` bug reproducer

Reproduces a Rust bug that prevents programs from compiling when `build-std-features = ["optimize_for_size"]` is used.

I have currently only tested this on macOS, where `nightly-2026-08-26` builds fine, but all newer versions as of today (`nightly-2026-09-12`) cause the following error:

```txt
error[E0152]: duplicate lang item in crate `core`: `sized`
  |
  = note: the lang item is first defined in crate `core` (which `std` depends on)
  = note: first definition in `core` loaded from $CARGO_BUILD_TARGET_DIR/debug/build/core/<hash>/out/libcore-<hash>.rmeta
  = note: second definition in `core` loaded from ~/.rustup/toolchains/nightly-2026-08-27-aarch64-apple-darwin/lib/rustlib/aarch64-apple-darwin/lib/libcore-<hash>.rmeta
```

If `build-std = ["std"]` is used without `build-std-features = ["optimize_for_size"]`, it builds successfully.