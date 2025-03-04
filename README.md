ARCANE RISC-V GNU Compiler Toolchain
=============================

This is the RISC-V C and C++ modified cross-compiler with custom instructions
for the POLITO ARCANE project. 

###  Getting the sources

This repository uses submodules, but submodules will fetch automatically on demand,
so `--recursive` or `git submodule update --init --recursive` is not needed.

    $ git clone https://github.com/Vincenzo-Petrolo/riscv-gnu-toolchain

**Warning: git clone takes around 6.65 GB of disk and download size**

### Prerequisites

Several standard packages are needed to build the toolchain.  

On Ubuntu, executing the following command should suffice:

    $ sudo apt-get install autoconf automake autotools-dev curl python3 python3-pip libmpc-dev libmpfr-dev libgmp-dev gawk build-essential bison flex texinfo gperf libtool patchutils bc zlib1g-dev libexpat-dev ninja-build git cmake libglib2.0-dev

On Fedora/CentOS/RHEL OS, executing the following command should suffice:

    $ sudo yum install autoconf automake python3 libmpc-devel mpfr-devel gmp-devel gawk  bison flex texinfo patchutils gcc gcc-c++ zlib-devel expat-devel
    
On Arch Linux, executing the following command should suffice:

    $ sudo pacman -Syyu autoconf automake curl python3 libmpc mpfr gmp gawk base-devel bison flex texinfo gperf libtool patchutils bc zlib expat

**Warning: Arch Linux is usually shipped with latest version of GCC, be sure to compile with gcc-9 if having problems**

On OS X, you can use [Homebrew](http://brew.sh) to install the dependencies:

    $ brew install python3 gawk gnu-sed gmp mpfr libmpc isl zlib expat texinfo flock

To build the glibc (Linux) on OS X, you will need to build within a case-sensitive file
system.  The simplest approach is to create and mount a new disk image with
a case sensitive format.  Make sure that the mount point does not contain spaces. This is not necessary to build newlib or gcc itself on OS X.

This process will start by downloading about 200 MiB of upstream sources, then
will patch, build, and install the toolchain.  If a local cache of the
upstream sources exists in $(DISTDIR), it will be used; the default location
is /var/cache/distfiles.  Your computer will need about 8 GiB of disk space to
complete the process.

### Installation

To build the Multilib cross-compiler, pick an install path (that is writeable).
If you choose, say, `/opt/riscv`, then add `/opt/riscv/bin` to your `PATH`.
Then, simply run the following command:

    ./configure --prefix=/opt/riscv --with-multilib-generator="rv32imczve32x_zicsr-ilp32--;rv32imc_zicsr-ilp32--;rv32i_zicsr-ilp32--"
    make

You should now be able to use riscv64-unknown-elf-gcc and its cousins.
