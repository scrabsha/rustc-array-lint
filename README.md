This repository aims to ease the debugging of [issue].

TLDR: running `cargo run` and `cargo build` report an error but not
`cargo check`.

# Disclaimer:

`cargo clean` has been run before issuing any of the following command.

# Working cases:

`build`ing or `run`ning the project, on stable, beta and nightly always fail
thanks to the `unconditional_panic` lint.

The generated error is:

```none
error: this operation will panic at runtime
 --> src/main.rs:4:20
  |
4 |     println!("{}", a[1]);
  |                    ^^^^ index out of bounds: the length is 1 but the index is 1
  |
  = note: `#[deny(unconditional_panic)]` on by default
```

# Failing cases:

Hitting `cargo run` (tested on stable, beta and nightly), however, builds fine,
without any error.

# Compiler version:

`rustc +nightly --version --verbose`:
```none
rustc 1.51.0-nightly (c5a96fb79 2021-01-19)
binary: rustc
commit-hash: c5a96fb7973649807a7943e7395456db158dcab6
commit-date: 2021-01-19
host: x86_64-unknown-linux-gnu
release: 1.51.0-nightly
LLVM version: 11.0.1
```

`rustc +beta --version --verbose`:
```none
rustc 1.50.0-beta.6 (ea20aa255 2021-01-14)
binary: rustc
commit-hash: ea20aa255b54708fb6a86f3146244eb20d079513
commit-date: 2021-01-14
host: x86_64-unknown-linux-gnu
release: 1.50.0-beta.6
```

`rustc --version --verbose`:
```none
rustc 1.49.0 (e1884a8e3 2020-12-29)
binary: rustc
commit-hash: e1884a8e3c3e813aada8254edfa120e85bf5ffca
commit-date: 2020-12-29
host: x86_64-unknown-linux-gnu
release: 1.49.0
```

[issue]: https://github.com/rust-lang/rust/issues/81224
