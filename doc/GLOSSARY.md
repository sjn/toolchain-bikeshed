## Terms

### Core Perl 6

The core perl distribution, including perl6 executable, any core modules, virtual machines and other requirements, as defined by the #perl6 community.

### OS

Operative System or distribution (e.g. RedHat Linux, Debian Linux, FreeBSD, Solaris, Microsoft Windows, Sailfish OS, etc.) running on a specified hardware platform.

### Installation sequence

"The Perl 6 module deployment stanza"

Consists of several steps. All of these should at some point be run, but they don't have to be run "at the same time". The sequence has the following steps:

- Fetch
- Unpack/Update source
- Check if dependencies are met
- Build
   - Create build directory
   - Apply patches
   - Generate files
   - Apply filters
   - Create precompiled library files
   - Populate the build directory with above files
- Pre-install test of everything in the build directory
- Install
    - Either Preparatory Install into a staging area (for Packaging)
    - Or OS Vendor Install (alongside/overriding system packages)
    - Or System Install
    - Or Core Install (e.g. into a Perl 6 implementation repository tree)
- Optional Install-tests
- Optional Post-install test, if tests and test dependencies have been installed
- Uninstall

### Pre-compilation

Perl modules can be compiled to bytecode, and cached to disk in order to speed up loading.

### Installation Scenarios

What are we trying to achieve when we install something?

- Module install
    - a simple module, nothing fancy going on here. File types may include .pm, .pm6, .pod, .pl and .pl6.
- Application install
    - Installation into a application location (e.g. /opt/company/appstack-1.0/...).  Files may include the same as in a Module install, plus any other file types found in a Application install. This may include modules, templates, static files, supporting binaries, internationalization files, ...
- Packaging install
    - Setting up a installation tree suitable to make a RPM or DEB package out of a Module install or an Application install.
- Image install
    - Installation of a Module install or Application install into a Docker image, chroot(1) jail, OpenSolaris container or equivalent.
    - The install has to be self-contained, without any unresolved external dependencies.

| Deployment Authority   | Scenario    | Target  | Precomp |
|------------------------|-------------|---------|---------|
| OS (vendor)            | Module      | system  | yes     |
| OS (vendor)            | Application | appdir  | yes     |
| OS (vendor)            | Packaging   | staging | yes     |
| OS (vendor)            | Image       | staging | yes     |
| Company (site)         | Module      | site    | yes     |
| Company (site)         | Application | appdir  | yes     |
| Company (site)         | Packaging   | staging | yes     |
| Company (site)         | Image       | staging | yes     |
| Developer (local)      | Module      | user    | no      |
| Developer (local)      | Application | user    | no      |
| Perl6 Community (core) | Module      | core    | yes     |

### Installation purpose

An installation as needed to fulfill a specific purpose. This may include:

- OS vendor preparation install (proposed better term: "System preparation install")
    - Installation as done by a packager, into a subtree that is later to be made into a system package (.rpm, .deb, etc.), intended for distro users or distro developers.
    - Used for Image, Packaging, Application and Module installs
- OS vendor install (proposed better term: "System install")
    - Installation of an .rpm, .deb, image prepared by someone doing the above step ("System preparation install" and subsequent packaging)
- Company site install (proposed better term: "Application install")
    - Installation intended for overriding/superseeding/adding to OS vendor installs without touching the actual vendor installs themselves. Used by companies and users.
    - Used for Image, Packaging, Application and Module installs
- Developer install (proposed better term: "Local install")
    - Installation into a user-specific tree, intended for that one specific user's development and testing purposes
    - Intended for Application and Module installs

### Source Location

The specific filesystem location and sub-directories where the software package intended to be installed, resides. The tree may be the result of one of the following actions:
- An extracted tarball
- A checked-out source code repository
- A URL pointing to a github repository (DISCUSS)
- An installed copy of the above options (used for "resetting" an existing/previous installation, if it somehow got modified) (DISCUSS)

### Build Location

A temporary directory used during the build step to put all files-to-be-installed in such a way that it mimics the final installation locations, taking into account any requested installation purpose.

This may be done by a simple copying from the source location, or by generating, patching or filter any relevant files in the source location. 

### Target location

The computed specific filesystem location used when copying files from a build location for a specific type of installation purpose.

### Software package

The module or application that we intend to install, as found in the Source Location

### Deployment authority

The packaging system used on a host system to do software installation, upgrades and other software managment tasks. Examples:

- Red Hat's RPM
- Debian's APT
- FreeBSD's PKG

### Source authority

The publisher of the software you are about to install. This may be the original author (doing a regular release), someone else (co-releasing or creating a fork) or yourself (creating a local patched version of an upstream release, before installation).

### Source package version

### Source API version

### Installation target index

A list containing directories where files classified as a specific type are expected to be installed (the expected target location for a file type). An index like this is system distribution specific, and intended to be vendor-, system- and user-overridable.

### Staging area

A directory intended to be used as a root for installation, instead of the normal root directory. The intention of installing into a staging area is to make it easy to create a package of the software so it may be installed with another installation authority.

# TODO

### CompUnitRepo

