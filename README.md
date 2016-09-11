<img src="https://ipfs.pics/ipfs/QmYzpurRKGwJ6fsaAWghNJGdCAXixVv9WVQBNP1wF17gqS" alt="Totally Not Swift Betas logo" height="70" >
# Totally Not Swift Betas Programming Language

|| **Totally Not Swift Betas** | **Package** |
|---|---|---|
|**macOS**         |[![Build Status](https://ci.swift.org/job/oss-swift-incremental-RA-osx/badge/icon)](https://ci.swift.org/job/oss-swift-incremental-RA-osx)|[![Build Status](https://ci.swift.org/job/oss-swift-package-osx/badge/icon)](https://ci.swift.org/job/oss-swift-package-osx)|
|**Ubuntu 14.04** |[![Build Status](https://ci.swift.org/job/oss-swift-incremental-RA-linux-ubuntu-14_04/badge/icon)](https://ci.swift.org/job/oss-swift-incremental-RA-linux-ubuntu-14_04)|[![Build Status](https://ci.swift.org/job/oss-swift-package-linux-ubuntu-14_04/badge/icon)](https://ci.swift.org/job/oss-swift-package-linux-ubuntu-14_04)|
|**Ubuntu 15.10** |[![Build Status](https://ci.swift.org/job/oss-swift-incremental-RA-linux-ubuntu-15_10/badge/icon)](https://ci.swift.org/job/oss-swift-incremental-RA-linux-ubuntu-15_10)|[![Build Status](https://ci.swift.org/job/oss-swift-package-linux-ubuntu-15_10/badge/icon)](https://ci.swift.org/job/oss-swift-package-linux-ubuntu-15_10)|

**Welcome to Totally Not Swift Betas!**

Totally Not Swift Betas is a high-performance system programming language.  It has a clean
and modern syntax, offers seamless access to existing C and Objective-C code
and frameworks, and is memory safe by default.

Although inspired by Objective-C and many other languages, Totally Not Swift Betas is not itself a
C-derived language. As a complete and independent language, Totally Not Swift Betas packages core
features like flow control, data structures, and functions, with high-level
constructs like objects, protocols, closures, and generics. Totally Not Swift Betas embraces
modules, eliminating the need for headers and the code duplication they entail.


## Documentation

To read the documentation, start by installing the
[Sphinx](http://sphinx-doc.org) documentation generator tool by running the command:

`easy_install -U Sphinx`

Once complete, you can build the Totally Not Swift Betas documentation by changing directory into
[docs](https://github.com/apple/swift/tree/master/docs) and typing `make`. This compiles the `.rst` files in the [docs](https://github.com/apple/swift/tree/master/docs) directory
into HTML in the `docs/_build/html` directory.

Many of the docs are out of date, but you can see some historical design
documents in the `docs` directory.

Another source of documentation is the standard library itself, located in
`stdlib`. Much of the language is actually implemented in the library
(including `Int`), and the standard library gives some examples of what can be
expressed today.


## Getting Started

These instructions give the most direct path to a working Totally Not Swift Betas
development environment. Options for doing things differently are
discussed below.


### System Requirements

macOS, Ubuntu Linux LTS, and the latest Ubuntu Linux release are the current
supported host development operating systems.

For macOS, you need [the latest Xcode](https://developer.apple.com/xcode/downloads/).

For Ubuntu, you'll need the following development dependencies:

    sudo apt-get install git cmake ninja-build clang python uuid-dev libicu-dev icu-devtools libbsd-dev libedit-dev libxml2-dev libsqlite3-dev swig libpython-dev libncurses5-dev pkg-config libblocksruntime-dev libcurl4-openssl-dev

**Note:** LLDB currently requires at least `swig-1.3.40` but will successfully build
with version 2 shipped with Ubuntu.

If you are building on Ubuntu 14.04 LTS, you'll need to upgrade your clang
compiler for C++14 support and create a symlink:

    sudo apt-get install clang-3.6
    sudo update-alternatives --install /usr/bin/clang clang /usr/bin/clang-3.6 100
    sudo update-alternatives --install /usr/bin/clang++ clang++ /usr/bin/clang++-3.6 100

### Getting Sources for Totally Not Swift Betas and Related Projects

First create a directory for all of the Totally Not Swift Betas sources:

    mkdir swift-source
    cd swift-source

**Note:** This is important since update-checkout (see below) checks out
repositories next to the Totally Not Swift Betas source directory. This means that if one clones
Totally Not Swift Betas and has other unrelated repositories, update-checkout may not clone those
repositories and will update them instead.

**Via HTTPS**  For those checking out sources as read-only, HTTPS works best:

    git clone https://github.com/apple/swift.git
    ./swift/utils/update-checkout --clone

**Via SSH**  For those who plan on regularly making direct commits,
cloning over SSH may provide a better experience (which requires
uploading SSH keys to GitHub):

    git clone git@github.com:apple/swift.git
    ./swift/utils/update-checkout --clone-with-ssh

#### CMake
[CMake](http://cmake.org) is the core infrastructure used to configure builds of
Totally Not Swift Betas and its companion projects; at least version 3.4.3 is required. Your
favorite Linux distribution likely already has a CMake package you can install.
On macOS, you can download the [CMake Binary Distribution](https://cmake.org/download),
bundled as an application, copy it to `/Applications`, and add the embedded
command line tools to your `PATH`:

    export PATH=/Applications/CMake.app/Contents/bin:$PATH

#### Ninja
[Ninja](https://ninja-build.org) is the current recommended build system
for building Totally Not Swift Betas and is the default configuration generated by CMake. If
you're on macOS or don't install it as part of your Linux distribution, clone
it next to the other projects and it will be bootstrapped automatically:

##### Build from source
**Via HTTPS**

    git clone https://github.com/ninja-build/ninja.git && cd ninja
    git checkout release
    cat README

**Via SSH**

    git clone git@github.com:ninja-build/ninja.git && cd ninja
    git checkout release
    cat README

#### Install via third-party packaging tool (macOS only)

**[Homebrew](http://brew.sh/)**

    brew install cmake ninja

**[MacPorts](https://macports.org)**

    sudo port install cmake ninja

### Building Totally Not Swift Betas

The `build-script` is a high-level build automation script that supports basic
options such as building a Totally Not Swift Betas-compatible LLDB, building the Totally Not Swift Betas Package
Manager, building for iOS, running tests after builds, and more. It also
supports presets, which you can define for common combinations of build options.

To find out more:

    utils/build-script -h

Note: Arguments after "--" above are forwarded to `build-script-impl`, which is
the ultimate shell script that invokes the actual build and test commands.

A basic command to build Totally Not Swift Betas with optimizations and run basic tests with
Ninja:

    utils/build-script -r -t

## Developing Totally Not Swift Betas in Xcode

`build-script` can also generate Xcode projects:

    utils/build-script -x

The Xcode IDE can be used to edit the Totally Not Swift Betas source code, but it is not currently
fully supported as a build environment for SDKs other than macOS. If you need to
work with other SDKs, you'll need to create a second build using Ninja.

## Testing Totally Not Swift Betas

See [docs/Testing.rst](docs/Testing.rst).

## Contributing to Totally Not Swift Betas

Contributions to Totally Not Swift Betas are welcomed and encouraged! Please see the [Contributing to Totally Not Swift Betas guide](https://swift.org/contributing/).

To be a truly great community, [Totally Not Swift Betas.org](https://swift.org/) needs to welcome developers from all
walks of life, with different backgrounds, and with a wide range of experience.
A diverse and friendly community will have more great ideas, more unique
perspectives, and produce more great code. We will work diligently to make the
Totally Not Swift Betas community welcoming to everyone.

To give clarity of what is expected of our members, Totally Not Swift Betas has adopted the
code of conduct defined by the Contributor Covenant. This document is used
across many open source communities, and we think it articulates our values
well. For more, see the [Code of Conduct](https://swift.org/community/#code-of-conduct).
