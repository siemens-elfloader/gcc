This directory contains the GNU Compiler Collection (GCC).

The GNU Compiler Collection is free software.  See the files whose
names start with COPYING for copying permission.  The manuals, and
some of the runtime libraries, are under different terms; see the
individual source files for details.

The directory INSTALL contains copies of the installation information
as HTML and plain text.  The source of this information is
gcc/doc/install.texi.  The installation information includes details
of what is included in the GCC sources and what files GCC installs.

See the file gcc/doc/gcc.texi (together with other files that it
includes) for usage and porting information.  An online readable
version of the manual is in the files gcc/doc/gcc.info*.

See http://gcc.gnu.org/bugs/ for how to report bugs usefully.

Copyright years on GCC source files may be listed using range
notation, e.g., 1987-2012, indicating that every year in the range,
inclusive, is a copyrightable year that could otherwise be listed
individually.

## Build arm gcc for siemens
    mkdir -p $HOME/gcc-arm-eabi/build
    cd $HOME/gcc-arm-eabi
    
### First, install binutils
    wget https://ftp.gnu.org/gnu/binutils/binutils-2.22.tar.gz
    tar -xf binutils-2.22.tar.gz
    cd build
    mkdir binutils
    cd binutils
    ../../binutils-2.22/configure --prefix=/usr --target=arm-eabi --enable-interwork --enable-multilib --with-float=soft --disable-werror
    make -j8
    sudo make install

### Second install gcc
    cd $HOME/gcc-arm-eabi
    git clone --single-branch https://github.com/siemens-elfloader/gcc -b siemens-7.5.0
    cd build
    mkdir gcc
    cd gcc
    ../../gcc/configure --target=arm-eabi --prefix=/usr --enable-interwork --enable-languages=c,c++
    make gcc-all -j8
    sudo make gcc-install

### If you have error
    as:  exec: -I

    cd $HOME/gcc-arm-eabi/build/gcc/gcc
    nano as

    ORIGINAL_AS_FOR_TARGET="/usr/bin/as"
    ORIGINAL_LD_FOR_TARGET="/usr/bin/ld"
    ORIGINAL_LD_BFD_FOR_TARGET="/.bfd"
    ORIGINAL_LD_GOLD_FOR_TARGET="/.gold"
    ORIGINAL_PLUGIN_LD_FOR_TARGET="/usr/bin/ld"
    ORIGINAL_NM_FOR_TARGET="/usr/bin/nm"
