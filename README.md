# Sarlin

Sarlin is an experimental general-purpose programming language with explicit,
readable syntax and native compilation. This public repository contains the
released compiler binaries, checksums, licenses and issue tracker. The compiler
source is developed privately and is not published here.

Version 0.1.0 is the first experimental release. Syntax and semantics may still
change, and it is not yet intended for production use.

## Download

The first release targets Linux x86_64. Download these files from the
[GitHub Releases](https://github.com/TheRealSarin/sarlin-lang/releases) page:

```text
sarlin-linux-x86_64.tar.gz
sarlin-linux-x86_64.tar.gz.sha256
```

Verify, extract and install the compiler:

```sh
sha256sum --check sarlin-linux-x86_64.tar.gz.sha256
tar -xzf sarlin-linux-x86_64.tar.gz
sudo install -m 755 sarlin /usr/local/bin/sarlin
sarlin --version
```

Sarlin needs `clang` 15 or newer to turn generated LLVM IR into a native
executable. Checking source code does not require clang.

## First project

```sh
sarlin new "My Project"
sarlin my_project
sarlin build my_project
./my_project/output/my_project
```

The generated `sarlin.project` marks the project root and records its required
`name` and `entry`, plus the current language compatibility version. Every
`.sar` file under its `source/` directory is compiled as part of the project.

The complete language guide and standard-library reference are at
[sarlin-lang.org](https://sarlin-lang.org).

## Issues and source availability

Use the [issue tracker](https://github.com/TheRealSarin/sarlin-lang/issues) for
bugs and feature requests. Compiler source and its development history remain
private; releases contain only the executable and license texts.

## License

Released binaries and this distribution repository are available under your
choice of the [MIT License](LICENSE-MIT) or the
[Apache License 2.0](LICENSE-APACHE): `MIT OR Apache-2.0`.
