# Building touchHLE

You need [git](https://git-scm.com/), [the Rust toolchain](https://www.rust-lang.org/tools/install), and your platform's standard C and C++ compilers.

First check out the git repo with `git clone`. Also make sure you get the submodules (`git submodule update --init` should be enough).

There is one special external dependency, Boost:

* On Windows, download it from <https://www.boost.org/users/download/> and extract the contents of the directory with a name like `boost_1_81_0` to `vendor/boost`.
* On other OSes, install Boost from your package manager. If you are on macOS and using [Homebrew](https://brew.sh/): `brew install boost`.

Then you just need to run `cargo run --release` (for a release build) or `cargo run` (for a debug build) to build and run touchHLE. On an underpowered, passively-cooled, 2-core laptop (2017 Retina MacBook), a clean release build takes a bit less than 9 minutes.

touchHLE can also be dynamically linked (which means instead of using the bundled dependencies, it will use the dependencies provided by your system). To build a dynamically linked version of touchHLE, you will need to have the SDL2 and OpenAL shared libraries installed, and then you can append `--no-default-features` (this flag is passed in to disable static linking, which is the default) to the end of the cargo build command. For macOS users: Apple's OpenAL.framework is not supported, only OpenAL Soft, and you need to add it to the linker path yourself.

The `touchHLE_dylibs` and `touchHLE_fonts` directories contain files that the resulting binary will need at runtime, so you'll need to copy them if you want to distribute the result. You also should include the license files.

If you're building touchHLE for the purpose of contributing, you might want to generate HTML documentation with `cargo doc --workspace --no-deps --open`. The code has been extensively commented with `cargo doc` in mind.
