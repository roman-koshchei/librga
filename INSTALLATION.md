# Rockchip RGA library

This fork is just to create backup and build/installation instructions.

To install you just need to copy library files and include files from this repo to your system.

Clone repository and enter it to later copy from it:

```bash
git clone https://github.com/roman-koshchei/librga && cd librga
```

Copy library files from `/libs/Linux/{your-architecture}`, my architecture (and likely yours) is `aarch64`, so:

```bash
sudo cp ./libs/Linux/gcc-aarch64/librga.a /usr/lib/ && sudo cp ./libs/Linux/gcc-aarch64/librga.so /usr/lib/ && sudo ldconfig
```

Copy include files into `/rga` subderictory:

```bash
sudo mkdir -p /usr/include/rga && sudo cp -r ./include/* /usr/include/rga/
```

Create package config file for library to be found:

```bash
sudo nano /usr/lib/pkgconfig/librga.pc
```

And paste this content:

```txt
prefix=/usr
exec_prefix=${prefix}
libdir=${exec_prefix}/lib
includedir=${prefix}/include

Name: librga
Description: Rockchip Graphics Accelerator Library
Version: 1.10.6
Libs: -L${libdir} -lrga
Cflags: -I${includedir}/rga
```

Then add it to package config path:

```bash
export PKG_CONFIG_PATH=/usr/lib/pkgconfig:$PKG_CONFIG_PATH
```

To verify:

```bash
pkg-config --modversion librga
```
