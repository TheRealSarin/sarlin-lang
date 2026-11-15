# Sarlin

Sarlin is an experimental general-purpose programming language designed to be easy to read. It compiles to native executables through LLVM and Clang.

I wanted to learn more about compilers, how they work and if I could make one. I also wanted a language that could do things the way I want it. 
So I made Sarlin. Sarlin is an acronym for my name, Florin Sarca and it's close enough to Starling to make me make the S out of birds for the logo. 

It's quite a decent little thing and thought why not share it with people

```sarlin
func greet(name string) string {
    return "Hello, " + name
}

func main() {
    print(greet("world"))
}
```

Sarlin includes explicit numeric types, strings, arrays, dictionaries, functions, classes assembled from reusable defines, callables, signals, checked arithmetic, basic TCP networking, project-wide source files, and embedded C, C++, and Rust functions.

Sarlin is still experimental. Its syntax and behaviour may change before a stable release, and it is not yet intended for production use.

## Download

Download the latest compiler from [GitHub Releases](https://github.com/TheRealSarin/sarlin-lang/releases/latest):

| Platform | Download |
| --- | --- |
| Linux x86-64 | `sarlin-linux-x86_64.tar.gz` |
| Linux ARM64 | `sarlin-linux-aarch64.tar.gz` |
| Windows x86-64 | `sarlin-windows-x86_64.zip` |
| Windows ARM64 | `sarlin-windows-aarch64.zip` |
| macOS Apple Silicon | `sarlin-macos-aarch64.tar.gz` |
| macOS Intel | `sarlin-macos-x86_64.tar.gz` |

Each download has a matching `.sha256` checksum file. Extract the archive, place `sarlin` or `sarlin.exe` somewhere on your `PATH`, then check the installation:

```text
sarlin --version
```

Clang 15 or newer is required when building Sarlin programs. Embedded C++ functions also require `clang++`, and embedded Rust functions require `rustc`. Checking Sarlin source without building it does not require these tools.

## First project

```sh
sarlin new "My Project"
sarlin check my_project
sarlin build my_project
sarlin run my_project
```

The executable is written to `my_project/output/my_project` on Linux and macOS, or `my_project/output/my_project.exe` on Windows.

Run `sarlin --help` to see all compiler commands. Passing a source file or project without a command remains shorthand for `sarlin check`.

Native builds are optimized by default. Add `--debug` for an unoptimized build with debug information, or `--output <path>` to choose the executable location.

## Compiler development

The repository keeps Rust formatting, Clippy, native runtime regressions, C warnings, and platform builds as CI gates. On Linux or macOS, run the full Sarlin/Rust benchmark comparison with:

```sh
./benchmarks/run.sh
```

Pass benchmark names to run a subset, or use `./benchmarks/run.sh --build-only` to validate every benchmark without executing the workloads.

## Documentation

Read the current language guide and standard-library reference at [sarlin-lang.org](https://sarlin-lang.org/).

## Issues and source availability

Use the [public issue tracker](https://github.com/TheRealSarin/sarlin-lang/issues) for bugs and feature requests. The compiler source and development history remain private; public releases contain the compiler executable and license texts.

## License

Released binaries and the public distribution repository are available under your choice of the [MIT License](https://github.com/TheRealSarin/sarlin-lang/blob/main/LICENSE-MIT) or the [Apache License 2.0](https://github.com/TheRealSarin/sarlin-lang/blob/main/LICENSE-APACHE): `MIT OR Apache-2.0`.

## Contributions

At the moment I am working on it by myself, not quite sure what I should do in the future, if it gets a huge comunity one day I will probably make the compiler open-source as well so people can contribute. But for now it is a passion project
