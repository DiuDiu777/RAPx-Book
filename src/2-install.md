# Chapter 2. Installation Guide

## Platform Support
* Linux
* macOS (both x86_64 and aarch64 version)

## Preparation
RAP is based on Rust version nightly-2024-06-30. You can install this version using the following command.
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
git clone https://github.com/Artisan-Lab/RAP.git
```

### Build and install RAP

```shell
./install.sh
```

You can combine the previous two steps into a single command:

```shell
cargo +nightly-2024-10-12 install rap --git https://github.com/Artisan-Lab/RAP.git
```

For macOS users, you may need to manually export Z3-related headers and libraries if you encounter compilation errors.
```
export C_INCLUDE_PATH=/opt/homebrew/Cellar/z3/VERSION/include:$C_INCLUDE_PATH
ln -s /opt/homebrew/Cellar/z3/VERSION/lib/libz3.dylib /usr/local/lib/libz3.dylib
```

After this step, you should be able to see the RAP plugin for cargo.
```
cargo --list
```

Execute the following command to run RAP and print the help message:
```
cargo rap -help
00:00:00|RAP|INFO|: 
Usage:
    cargo rap [rap options] -- [cargo check options]

Rap Options:

Use-After-Free/double free detection.
    -F or -uaf       command: "cargo rap -uaf"

Memory leakage detection.
    -M or -mleak     command: "cargo rap -mleak"

Debugging options:
    -mir             print the MIR of each function

General command: 
    -H or -help:     show help information
    -V or -version:  show the version of RAP
...
```

### Uninstall
```
cargo uninstall rap
```
