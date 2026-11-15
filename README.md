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

## Upgrading

```sh
sarlin upgrade --check
sarlin upgrade
```

`sarlin upgrade --check` only reports whether a newer release exists. `sarlin upgrade` downloads the archive for your platform from the latest GitHub release, verifies its SHA-256 checksum against the published `.sha256` file, checks that the new binary reports the expected version, and then replaces the installed `sarlin`. Nothing is changed if any check fails. The network is used only by `sarlin upgrade`, never by other commands.

If the install directory is not writable, Sarlin does not ask for elevated privileges. It saves the verified binary as `sarlin-<version>` in the current directory and tells you where it is, so you can copy it into place with the permissions your system requires. `sarlin upgrade` needs `curl` and `tar` on your path.

## Packages

Packages are ordinary Sarlin projects published on GitHub and listed in the [Nook](https://github.com/TheRealSarin/sarlin-nook). Run these from a project folder, or pass the project folder as the last argument. They need `git` on your `PATH`.

```sh
sarlin add acras
sarlin add acras@0.3.0
sarlin add github.com/owner/repo
sarlin remove acras
sarlin update
sarlin collisions
```

`add` records `require: acras 0.3.0` in `sarlin.project` (exact versions only). Packages added straight from GitHub are recorded with their address, as `require: name 1.0.0 https://github.com/owner/repo`. `update` moves every required package to its newest version.

`collisions` lists every name defined in more than one file across your project and its packages, since duplicate names stop a build. It prints `no collisions found` and exits with status 0 when clean, or one `warning:` line per name plus a summary and status 1, so CI can use it. It also reports a package that defines `func main`. `add` and `update` run the same check and print the warnings without failing.

`sarlin.lock` sits next to `sarlin.project` and pins every package, including packages that other packages require, to a commit. Commit it with your project. `check`, `build` and `run` fetch any missing package at its locked commit, and compile each package's `source/` files together with your own. A package must not define `func main`. Projects without `require:` lines never use git.

Downloaded packages are cached in `~/.sarlin/nook` (`%USERPROFILE%\.sarlin\nook` on Windows). Set `SARLIN_NOOK_HOME` to move the cache, or `SARLIN_NOOK_INDEX` to read the package list from another git repository.

## Editor support

The Sarlin extension for VSCodium and VS Code adds syntax colouring, a colour picker for hexadecimal colour values, and a file icon for `.sar` files. Download [sarlin-language.vsix](https://github.com/TheRealSarin/sarlin-editors/releases/latest/download/sarlin-language.vsix) and install it:

```sh
codium --install-extension sarlin-language.vsix
```

The extension source lives in [sarlin-editors](https://github.com/TheRealSarin/sarlin-editors).

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
