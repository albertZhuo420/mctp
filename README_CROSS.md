# meson cross compile

使用meson进行交叉编译必须的有一个cross-compile的配置文件, **该文件的名字和后缀没有任何限制**;

- meson cross compile config file: **`meson.cross`**

  ```sh
  [host_machine]
  system = 'linux'
  cpu_family = 'arm'
  cpu = 'arm'
  endian = 'little'
  
  [binaries]
  c = 'arm-buildroot-linux-gnueabihf-gcc'
  cpp = 'arm-buildroot-linux-gnueabihf-g++'
  ar = 'arm-buildroot-linux-gnueabihf-gcc-ar'
  ld = 'arm-buildroot-linux-gnueabihf-ld'
  objcopy = 'arm-buildroot-linux-gnueabihf-objcopy'
  strip = 'arm-buildroot-linux-gnueabihf-strip'
  ```

  - 参考链接: 

    [meson 交叉编译](https://blog.csdn.net/xys616/article/details/116756444);

    [Compilation and Installation Using Meson](https://docs.mesa3d.org/meson.html);

    [使用meson交叉编译glib库的过程](https://blog.csdn.net/xiaolz88/article/details/129999608);

  - **`host_machine`**: 

    https://mesonbuild.com/Cross-compilation.html;

    Provides information about the host machine -- the machine on which the compiled binary will run.

  - **binaries**: 这个参数的填写需要根据source的sdk中的变量来填写:

    ```sh
    $ printenv | grep arm-buildroot-linux-gnueabihf
    CPPFLAGS_FOR_BUILD=-I/home/zhuo/work/cross-toolchain/arm-buildroot-linux-gnueabihf_sdk-systemd/include
    STAGING_DIR=/home/zhuo/work/cross-toolchain/arm-buildroot-linux-gnueabihf_sdk-systemd/arm-buildroot-linux-gnueabihf/sysroot
    LDFLAGS_FOR_BUILD=-L/home/zhuo/work/cross-toolchain/arm-buildroot-linux-gnueabihf_sdk-systemd/lib -Wl,-rpath,/home/zhuo/work/cross-toolchain/arm-buildroot-linux-gnueabihf_sdk-systemd/lib
    CPP=arm-buildroot-linux-gnueabihf-cpp
    CFLAGS_FOR_BUILD=-O2 -I/home/zhuo/work/cross-toolchain/arm-buildroot-linux-gnueabihf_sdk-systemd/include
    CXX=arm-buildroot-linux-gnueabihf-g++
    LD=arm-buildroot-linux-gnueabihf-ld
    READELF=arm-buildroot-linux-gnueabihf-readelf
    DEFAULT_ASSEMBLER=arm-buildroot-linux-gnueabihf-as
    F77=arm-buildroot-linux-gnueabihf-gfortran
    AR=arm-buildroot-linux-gnueabihf-gcc-ar
    AS=arm-buildroot-linux-gnueabihf-as
    CXXFLAGS_FOR_BUILD=-O2 -I/home/zhuo/work/cross-toolchain/arm-buildroot-linux-gnueabihf_sdk-systemd/include
    NM=arm-buildroot-linux-gnueabihf-gcc-nm
    GCC=arm-buildroot-linux-gnueabihf-gcc
    OBJCOPY=arm-buildroot-linux-gnueabihf-objcopy
    FC=arm-buildroot-linux-gnueabihf-gfortran
    DEFAULT_LINKER=arm-buildroot-linux-gnueabihf-ld
    STRIP=arm-buildroot-linux-gnueabihf-strip
    OBJDUMP=arm-buildroot-linux-gnueabihf-objdump
    PATH=/home/zhuo/work/cross-toolchain/arm-buildroot-linux-gnueabihf_sdk-systemd/bin:/home/zhuo/work/cross-toolchain/arm-buildroot-linux-gnueabihf_sdk-systemd/sbin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin
    CC=arm-buildroot-linux-gnueabihf-gcc
    CROSS_COMPILE=arm-buildroot-linux-gnueabihf-
    CONFIGURE_FLAGS=--target=arm-buildroot-linux-gnueabihf --host=arm-buildroot-linux-gnueabihf --build=x86_64-pc-linux-gnu --prefix=/usr --exec-prefix=/usr --sysconfdir=/etc --localstatedir=/var --program-prefix=
    RANLIB=arm-buildroot-linux-gnueabihf-gcc-ranlib
    _=/home/zhuo/work/cross-toolchain/arm-buildroot-linux-gnueabihf_sdk-systemd/bin/printenv
    ```

此项目的编译命令是:

```sh
$ meson setup build --cross-file meson.cross
```

