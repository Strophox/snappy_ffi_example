# snappy_ffi_example
Testing Rust's and Miri's FFI capabilities.

As of writing, this is also the main FFI example used in [The Rustonomicon](https://doc.rust-lang.org/nomicon/ffi.html).

## How to run/test

To run the tests this crate requires a compiled version of [Google/snappy](https://github.com/google/snappy).

*(Note: To compile an `.so`, I had to locate and change the line in `CMakeLists.txt` to `option(BUILD_SHARED_LIBS "Build shared libraries(DLLs)." ON)` (i.e. `OFF` -> `ON`))*

*(Note: I also found a precompiled version of snappy e.g. on <https://anaconda.org/conda-forge/snappy/files>.)*

### Testing normally

To test normally:
1. Have `libsnappy.a` or `libsnappy.so` in the project root directory.
2. Run `cargo test`

### Testing with Miri

To test with Miri from the nightly toolchain:
1. Have `libsnappy.so` in the project root directory.
2. Install Miri with `rustup +nightly component add miri`
3. Run `MIRIFLAGS="-Zmiri-native-lib=./libsnappy.so" cargo +nightly miri test`
