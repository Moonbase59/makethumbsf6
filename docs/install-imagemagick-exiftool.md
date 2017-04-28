# Installing ImageMagick and Exiftool for Ubuntu 14.04/16.04 and Linux Mint 17.x/18.x

_2017-04-29 – Matthias C. Hormann_

**This is _only_ needed if you don’t have the tools already installed.**


## ImageMagick

Check if it’s already installed:

```bash
$ identify -version
Version: ImageMagick 7.0.5-5 Q16 x86_64 2017-04-23 http://www.imagemagick.org
Copyright: © 1999-2017 ImageMagick Studio LLC
License: http://www.imagemagick.org/script/license.php
Features: Cipher DPC HDRI OpenMP
Delegates (built-in): freetype jbig jng jpeg lzma png tiff webp x xml zlib
```

If your system instead responds with `command not found`, you need to install ImageMagick as follows:

```bash
$ sudo apt-get install imagemagick
```


## Exiftool

Check if it’s already installed:

```bash
$ exiftool -ver
10.10
```

If your system instead responds with `command not found`, you need to install Exiftool as follows:

```bash
$ sudo apt-get install libimage-exiftool-perl perl-doc
```


**Enjoy!**
