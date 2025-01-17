# Chapter 2. Installation Guide

## Platform Support
* Linux
* macOS (both x86_64 and aarch64 version)

## Preparation
RAPx is based on Rust version nightly-2024-10-12. You can install this version using the following command.
```shell
rustup toolchain install nightly-2024-10-12 --profile minimal --component rustc-dev,rust-src,llvm-tools-preview
```

If you have multiple Rust versions, please ensure the default version is set to nightly-2024-06-30.
```
rustup show
```

## Install
### Download the project
```shell
git clone https://github.com/Artisan-Lab/RAPx.git
```

### Build and install RAPx

```shell
./install.sh
```

You can combine the previous two steps into a single command:

```shell
cargo +nightly-2024-10-12 install rapx --git https://github.com/Artisan-Lab/RAPx.git
```

For macOS users, you may encounter compilation errors related to Z3 headers and libraries. There are two solutions:

The first one is to manually export the headers and libraries as follows:
```
export C_INCLUDE_PATH=/opt/homebrew/Cellar/z3/VERSION/include:$C_INCLUDE_PATH
ln -s /opt/homebrew/Cellar/z3/VERSION/lib/libz3.dylib /usr/local/lib/libz3.dylib
```

Alternatively, you can modify the [Cargo.toml](https://github.com/Artisan-Lab/RAPx/blob/main/rapx/Cargo.toml) file to change the dependency of Z3 to use static linkage. However, this may significantly slow down the installation process, so we do not recommend enabling this option by default.

```
[dependencies]
z3 = {version="0.12.1", features = ["static-link-z3"]}
```

After this step, you should be able to see the RAPx plugin for cargo.
```
cargo --list
```

Execute the following command to run RAPx and print the help message:
```
cargo rapx -help
00:00:00|RAP|INFO|: 
Usage:
    cargo rapx [rapx options] -- [cargo check options]

RAPx Options:

Use-After-Free/double free detection.
    -F or -uaf       command: "cargo rapx -uaf"

Memory leakage detection.
    -M or -mleak     command: "cargo rapx -mleak"

Debugging options:
    -mir             print the MIR of each function

General command: 
    -H or -help:     show help information
    -V or -version:  show the version of RAPx
...
```

### Uninstall
```
cargo uninstall rap
```
