# ImageMagick update for Ubuntu 14.04/16.04 and Linux Mint 17.x/18.x

_2017-04-28 – Matthias C. Hormann_

**Perform this step _only_ if you need to convert _animated GIFs_ and your ImageMagick version is so old that it produces GIFs that look like 4 images stacked on top of each other.**

For instance, the image `080-Night-lights-in-Europe.gif` from the `sample-gallery` _should_ look like this when converted to the »small« version:

![s/080-Night-lights-in-Europe.s.gif](good.gif)

Your ImageMagick version is too old when it looks like this instead:

![s/080-Night-lights-in-Europe.s.gif](bad.gif)

---

Unfortunately, on Ubuntu and derivatives like Linux Mint, we need to compile and install a newer ImageMagick version directly from the sources, because there is no current ready-made package.

But it’s not that complicated and I’ll show you how to do it. To start, just open a terminal and enter the following command:

```bash
sudo apt-get install build-essential checkinstall \
             libx11-dev libxext-dev zlib1g-dev libpng12-dev \
             libjpeg-dev libfreetype6-dev libxml2-dev
```

To get all build dependencies, we need to activate the system’s source code repos:

#### Ubuntu

Go to _Dash → Software & Updates → Source Code_.

#### Linux Mint (English)

Go to _Menu → Administration → Software Sources → (password) → [x] Enable source code repositories_.

#### Linux Mint (German)

Go to _Menü → Anwendungspaketquellen → (Passwort) → [x] Quelltextpaketquellen aktivieren)_.

Now we can get the build dependencies:

```bash
sudo apt-get build-dep imagemagick
```

We will make our own directory for the source code install. Eventually, we will also create a `.deb` package here to make future (re-)installs just a little easier.

```bash
mkdir $HOME/imagemagick_build
cd $HOME/imagemagick_build
```

Now we get the current version from ImageMagick, as a compressed archive, and unpack it:

```bash
wget http://www.imagemagick.org/download/ImageMagick.tar.gz
tar xvf ImageMagick.tar.gz
```

**Attention:** For the next commands, always use the _actual version number_ you downloaded instead of `7.0.5-5` which was current at the time of this writing.

```bash
cd ImageMagick-7.0.5-5
./configure --enable-shared
make
```

Use the actual version for the next command again. We will now check and actually perform the install and at the same time generate a `.deb` package with our ImageMagick version for future reference:

```bash
sudo checkinstall -D --install=yes --fstrans=no --pakdir "$HOME/imagemagick_build" \
     --pkgname imagemagick --backup=no --deldoc=yes --deldesc=yes --delspec=yes --default \
     --pkgversion "7.0.5-5"
```

Now, let’s configure dynamic linker run-time bindings:

```bash
sudo ldconfig
```

And clean up …

```bash
make distclean
```

To check if everything went well:

```bash
identify -version
Version: ImageMagick 7.0.5-5 Q16 x86_64 2017-04-27 http://www.imagemagick.org
Copyright: © 1999-2017 ImageMagick Studio LLC
License: http://www.imagemagick.org/script/license.php
Features: Cipher DPC HDRI OpenMP
Delegates (built-in): bzlib djvu fftw fontconfig freetype jbig jng jpeg lcms lqr lzma openexr pangocairo png tiff wmf x xml zlib
```

It should respond with something like the above. (If it doesn’t, try logging off and back on again, then retry.)

**Done!** We have now compiled an updated ImageMagick all by ourselves. It wasn’t that hard, was it?
