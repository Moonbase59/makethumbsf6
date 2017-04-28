# makethumbsf6



## Make thumbnails, responsive images and HTML/Zurb Foundation 6 markup all in one go!

A _bash_ script, put it into `~/bin`, `chmod +x makethumbsf6` and for a first (standalone) trial run start it from _inside_ the `sample-gallery` folder.

It should create a set of subfolders:

* `t` — thumbnails, original aspect ratio
* `ts` — squared & cropped thumbnails, 120x120px
* `s` — responsive images for small screens (320w)
* `m` — responsive images for medium screens (640w)
* `l` — resonsive images for large screens (1024w)
* `xl` — responsive images for extra-large screens (1920w)


### What’s new in version 0.9.2?

* **Assistive technologies** for people with disabilities: Added some button descriptions and more [ARIA](https://www.w3.org/WAI/intro/aria) labels. Generated markup now passes [WAVE](http://wave.webaim.org/) test.

* _Makethumbsf6_ now uses **Foundation’s »thumbnail« class** for the generated thumbnail links. This makes the visual presentation _more attractive_, is _more compatible_ with _Foundation 6_ and allows for _easy overall changes_ within the framework. (See also http://foundation.zurb.com/sites/docs/thumbnail.html.)

* Generated thumbnail markup now has **proper ARIA labels**.

* Added some documentation on how to [install/update ImageMagick and exiftool](#installation-update-of-imagemagick-exiftool).

**What else is new?** See the [changelog](#changelog-of-sorts). Or check out the auto-generated [sample page](http://kaufen-ist-toll.de/demos/mkthumbsf6/sample-gallery/).


### Standalone

If run within a »normal« image folder, _makethumbsf6_ will also generate a **HTML sample file** with a **[PhotoSwipe](http://photoswipe.com/) lightbox** and almost all **documentation included**.

_You can use this to copy-and-paste actual responsive images and markup code for your website, or just for creating a nice slide show on the fly._

### ZURB Foundation 6 Frontend Framework

If run inside a **[ZURB Foundation 6](http://foundation.zurb.com/)** folder structure (i.e, something like `src/assets/img/gallery/album-01/…`), it will instead generate a **ready-to-run partial** inside your `src/partials` folder. You can simply include this partial on a gallery page using Panini, for example as `{{> gallery-gallery-album-01 gid=1}}`.

_You typically use this when working on projects using the Foundation framework, but the generated markup can easily be adapted for other frameworks._

### Automatic headlines, image captions and markup comments

I strongly believe that image information should be stored together with the image (much like we do it with FLAC or MP3 files already). The image files can then be copied, moved, put on the web without the need of updating databases, changing HTML markup manually, and even the image credits will still be in place if someone downloads it.

Like image and news agencies already do for a long time, I encourage you to store data like a **headline**, a **caption text**, the **photographer’s name** and a **copyright notice** _inside_ your images. You can use tools like _exiftool_ (or many others) for that, or Adobe Photoshop, Adobe Lightroom, even Windows’ image properties or Mac OSX’ Finder.

Some modern professional cameras (Nikon come to mind) already allow setting your name and copyright line _in the camera settings_, so this information will automatically be stored with each shot you take.

_Makethumbsf6_ will _automatically_ read this data, and present you with a beautiful and customizable view. It’ll even generate _map links_ for you, if the **GPS location** is stored in the images (like many new cameras and smartphones do).

Additionally, _makethumbsf6_ will automatically put the photographer’s name and (if specified) additional image credits (like maybe the image agency’s name) next to your caption text. This makes it super-easy for you to follow licensing or local laws, if so required.

**Run _makethumbsf6_ inside the `sample-gallery` folder, then view the generated HTML file with your browser.** All sample images have tags (some even GPS data) so you can get a first idea of what can be done. Feel free to change some tags within the sample images (maybe using _exiftool_ or another application you prefer), then run _makethumbsf6_ again to see what’s changed.

#### Image tags currently known and used by _makethumbsf6_:

For all tags, we follow the strict fallback rule: _EXIF → IPTC → XMP_. This means, if there is an EXIF tag, we use it. If not, we fall back to IPTC data, and as a last measure to XMP.

Here is a prioritized list of tags from which we read the image data:

* CREATOR: `exif:artist`, `by-line`, `creator`

* CREDIT: `credit`, `publisher`

* DESCRIPTION: `exif:imagedescription`, `caption-abstract`, `description`, `XPcomment`

* HEADLINE: `headline`, `objectname`, `title`

* KEYWORDS: `keywords`, `subject`

* COPYRIGHT: `exif:copyright`, `copyrightnotice`, `rights`

* DATE: `dateTimeOriginal`

* LOCATION: `gpslatitude`, `gpslongitude`, `gpsaltitude`, `gpsimgdirection`



## Generated markup

### Example: Thumbnail with link to a lightbox script.

This example has a filename using foreign characters (URL-encoded where necessary), quite a long description, both photographer’s name and credits in it’s data, IMAGE_LINKTO="xl", USE_MAPS=true, MAPLINK_TEXT="Show on map (Google Maps)". It also features a copyright notice and GPS data (latitude, longitude, altitude and viewing direction).

All data read from the actual image is safely encoded using HTML entities (instead of using simple UTF-8), so there’s no possibility that characters like `"`, `'`, `<`, `>` and others could break your code or open any security holes.

```html
<!-- 040-winter-in-bad-grönenbach.jpg (1920x2560px) - cropped, square thumbnail with link to original image -->
<!-- Image copyright: Copyright &copy; 2016 Matthias C. Hormann, all rights reserved. Alle Rechte vorbehalten. -->
<!-- Image location: 47.8521118055556,10.1619062222222 Height: 732m Viewing direction: 40° -->
<figure itemprop="associatedMedia" itemscope itemtype="http://schema.org/ImageObject" title="Eisesk&auml;lte in Bad Gr&ouml;nenbach">
  <a href="xl/040-winter-in-bad-gr%C3%B6nenbach.xl.jpg" itemprop="contentUrl" data-size="1920x2560">
    <img src="ts/040-winter-in-bad-gr%C3%B6nenbach.ts.jpg" itemprop="thumbnail" alt="Eisesk&auml;lte in Bad Gr&ouml;nenbach">
  </a>
  <figcaption itemprop="caption description" title="Eisesk&auml;lte in Bad Gr&ouml;nenbach"><h4>Eisesk&auml;lte in Bad Gr&ouml;nenbach</h4><p><span itemprop="dateCreated" content="2016-12-22T11:17:09">2016-12-22</span> — Trotz Sonnenschein herrschte im Dezember in Bad Gr&ouml;nenbach und Umgebung eine klirrende K&auml;lte &ndash; bis zu -21 &deg;C wurden gemessen. Auf der Kreisstra&szlig;e zwischen Bad Gr&ouml;nenbach und Legau entdeckte unser Fotograf diesen vom Eis verzauberten Baum am Stra&szlig;enrand. [This is an example for UTF-8-encoded foreign text and auto-generated map links.] <span class="imagecredits">(Photo: Matthias C. Hormann / M. Hormann Webdesign)</span></p><a href="https://maps.google.com/maps?t=m&amp;q=47.8521118055556,10.1619062222222" rel="nofollow" target="_blank">Show on map (Google Maps)</a></figcaption>
</figure>
```

When auto-generating a _Foundation 6 partial_, the script will have these active. On thumbnails, the _caption is often suppressed_ via CSS:

```css
.gallery figcaption {
  display: none;
}
```

The _credits_ in the lightbox can also be displayed on a new line, using a slightly smaller font:

```css
/* Make image credits a little smaller, on a new line */
.imagecredits {
  font-size: 80%;
}
.imagecredits:before {
  content: '\A';
  white-space: pre;
}
```

### Example: Same image, responsive, fullsize.

This shows the generated HTML for the same image, fullsize, with responsive markup (using a `srcset`, so the user’s browser decides which image to actually load; this also neatly solves all problems with Retina displays and the like):

```html
<!-- 040-winter-in-bad-grönenbach.jpg (1920x2560px) - "normal" image on a page, with a srcset (responsive loading) -->
<!-- Image copyright: Copyright &copy; 2016 Matthias C. Hormann, all rights reserved. Alle Rechte vorbehalten. -->
<!-- Image location: 47.8521118055556,10.1619062222222 Height: 732m Viewing direction: 40° -->
<figure itemprop="associatedMedia" itemscope itemtype="http://schema.org/ImageObject" title="Eisesk&auml;lte in Bad Gr&ouml;nenbach">
  <img srcset="
      s/040-winter-in-bad-gr%C3%B6nenbach.s.jpg 320w,
      m/040-winter-in-bad-gr%C3%B6nenbach.m.jpg 640w,
      l/040-winter-in-bad-gr%C3%B6nenbach.l.jpg 1024w,
      xl/040-winter-in-bad-gr%C3%B6nenbach.xl.jpg 1920w
      "
    src="s/040-winter-in-bad-gr%C3%B6nenbach.s.jpg"
    sizes="
      100vw"
    alt="Eisesk&auml;lte in Bad Gr&ouml;nenbach">
  <figcaption itemprop="caption description" title="Eisesk&auml;lte in Bad Gr&ouml;nenbach"><h4>Eisesk&auml;lte in Bad Gr&ouml;nenbach</h4><p><span itemprop="dateCreated" content="2016-12-22T11:17:09">2016-12-22</span> — Trotz Sonnenschein herrschte im Dezember in Bad Gr&ouml;nenbach und Umgebung eine klirrende K&auml;lte &ndash; bis zu -21 &deg;C wurden gemessen. Auf der Kreisstra&szlig;e zwischen Bad Gr&ouml;nenbach und Legau entdeckte unser Fotograf diesen vom Eis verzauberten Baum am Stra&szlig;enrand. [This is an example for UTF-8-encoded foreign text and auto-generated map links.] <span class="imagecredits">(Photo: Matthias C. Hormann / M. Hormann Webdesign)</span></p><a href="https://maps.google.com/maps?t=m&amp;q=47.8521118055556,10.1619062222222" rel="nofollow" target="_blank">Show on map (Google Maps)</a></figcaption>
</figure>
```

In the _standalone version_, the generated HTML page will also show this image so you can verify that everything loads as expected.

When generating a _Foundation 6 partial_, the fullsize image markup will _also be included, but commented out_. This allows to copy-paste perfect responsive image markup for other places on your website. Usually, when generating the production version, the HTML will run through some minification process anyway and the comment be cleaned out automatically, so no overhead is generated for the production site. (Check your _gulpfile.babel.js_ and _htmlmin_.)

## Customization: Have _makethumbsf6_ do what _you_ need!

My script is highly customizable and each option very well documented. Just make a backup, then open the `makethumbsf6` script with a normal (UTF-8-capable) text editor and have a peek inside.

You’ll find a lot of customization options that you can change to fit _your_ needs. Here are just a very few:

* **USE_SQUARE_THUMBS**: Use square thumbnails (auto-cropped), or »normal« ones (having the same aspect ratio as the original image)?

* **USE_LIGHTBOX**: For the standalone version, include the _PhotoSwipe_ lightbox?

* **FIGURE_TITLE**: Force the same title for all thumbnails (i.e., »Click to magnify« instead of the image’s headline)?

* **IMAGE_LINKTO**: Link to the original image or to some defined (max.) size like "xl"?

* **USE_DATE, DATEFORMAT, DATE_LEADOUT**: Define if the »image taken on« date should be shown, and in which format.

* **CREDITS_LEADIN, CREDITS_LEADOUT**: Put some nice text around the image credits (i.e. »(Photo: Photographer / Agency)« instead of »Photographer / Agency«)?

* **USE_MAPS, MAPLINK_TEXT**: Use map links if image has GPS data? What text to display?

* **F_NAME, F_BREAKPOINT, F_CONV**: Number and names of different image versions to generate, their (or your framework’s) responsive breakpoints, and even the commands for each resolution to be given to ImageMagick’s `convert`.

* **F_CHANGETYPE**: Convert one filetype to another, i.e. TIFF → JPEG on the fly.

* … and many, many more!

The generated HTML markup has **_schema.org_ microdata**, is **SEO-optimized**, and **_valid_**. You can easily change lots of display options using pure **CSS**.

Please read the documentation in the HTML file generated when you run _makethumbsf6_ inside the `sample-gallery` folder. Just below the images, there’s lots and lots of valuable information to find!

**No need to do the tedious stuff manually again. Ever.**

_Hint:_ For performance reasons, _makethumbsf6_ will skip already-made thumbnails and lower-res images when it is run again. If you want to _force_ it, just delete the above-mentioned subfolders.

---

More documentation will follow. Meanwhile, have fun reading the sample HTML file. ;-)

_The script (makethumbsf6) is MIT licensed, the images in the sample gallery are NOT (though many of them are CC0). Please check the image data and/or the generated HTML code which will show the copyright notices. **Thank you.**_

Drop me a line [@Moonbase59](https://twitter.com/intent/tweet?text=%40Moonbase59&amp;hashtags=makethumbsf6) and let me know what you think. Or [let others know, too](https://twitter.com/intent/tweet?text=Easily%20make%20thumbs%2C%20responsive%20images%2C%20HTML%20markup&url=https%3A%2F%2Fgithub.com%2FMoonbase59%2Fmakethumbsf6&via=Moonbase59&hashtags=makethumbsf6,thumbnails,responsive,foundation)!



## Requirements

* A _Linux-type OS_ that has a _bash_ shell with array support and can do 'sort -z'. This means you should be able to use this script on **nearly any Linux machine** as well as on **Apple products** running **Mac OS X** (starting with 10.3 »Panther«), **OS X** and **macOS Sierra**.
* [ImageMagick](https://www.imagemagick.org/)
* [Exiftool](http://www.sno.phy.queensu.ca/~phil/exiftool/)

* For changes and setting options: A text editor that handles UTF-8 (no BOM please).



## Installation/Update of ImageMagick/Exiftool

### Ubuntu, Linux Mint

* [Installing ImageMagick and Exiftool for Ubuntu 14.04/16.04 and Linux Mint 17.x/18.x](docs/install-imagemagick-exiftool.md)

* [ImageMagick update for Ubuntu 14.04/16.04 and Linux Mint 17.x/18.x](docs/imagemagick-update.md)


### RedHat/CentOS

* There will most probably be RPMs in your system’s repositories. Alternatively, follow the installation instructions on [ImageMagick’s](https://www.imagemagick.org/script/binary-releases.php) and [Exiftool’s](http://www.sno.phy.queensu.ca/~phil/exiftool/) homepages.


### Other Linuxes

* First, try to verify if both tools are installed by doing a `identify -version` for _ImageMagick_ and `exiftool -ver` for _exiftool_ in a terminal window.

* If they are not, try to locate them in your repositories, using the appropriate package or software manager. Preferably install from there.

* If all else fails, follow the installation instructions on [ImageMagick’s](https://www.imagemagick.org/script/binary-releases.php) and [Exiftool’s](http://www.sno.phy.queensu.ca/~phil/exiftool/) homepages.


### FreeBSD

* The good news: _Yes,_ I’ve seen it working on FreeBSD.

* The bad news: Since _bash_ is neither the default shell nor even included in the default FreeBSD installation, you’ll have to install _bash_ + _ImageMagick_ + _exiftool_ + _makethumbsf6_. Then `chsh` to bash and use it.

* It might still be worth the effort. Thanks for considering.


### Mac OS X

* Follow the installation instructions on [ImageMagick’s](https://www.imagemagick.org/script/binary-releases.php) and [Exiftool’s](http://www.sno.phy.queensu.ca/~phil/exiftool/) homepages.


# Windows

* A _bash script_ like _makethumbsf6_ will not work on the Windows command line, sorry for that. I invite you to study the code nevertheless—maybe it’s _you_ who comes up with a Windows equivalent?

* You might still want to get _ImageMagick_ and _exiftool_. Follow the installation instructions on [ImageMagick’s](https://www.imagemagick.org/script/binary-releases.php) and [Exiftool’s](http://www.sno.phy.queensu.ca/~phil/exiftool/) homepages.



## Changelog (of sorts)

### Version 0.9.1

* **Safety first**: You never know what users come up with … Fancy filenames using »illegal« characters like `'`, `"`, `:`, `[`, `]`, `$` and so forth now work again and **don’t break _makethumbsf6_**. Try something like »`Fancy: Filename $["ÄÖÜß'] $25.00.jpg`«.

* For smaller images (width smaller than the largest breakpoint specified), there are **no duplicate `srcset` widths generated anymore**. Duplicate widths in a `srcset` prevent validation, and we want our HTML to validate at all times.


### Version 0.9.0

* **Animated GIFs** are now handled (and resized) correctly. _Hint:_ If the generated lower resolution images look like 4 images on top of each other, you might want to upgrade your _ImageMagick_ to a newer version.

* _Makethumbsf6_ now also handles **TIFF** (.tif, .tiff) files. Per default, these will be automatically **converted to JPEG** images (smaller, browsers can display them).

* You can now specify image **type conversion**, i.e. convert **TIFF to JPEG**, **MPO to JPEG** and so forth. For purely aesthetic reasons, `.jpeg` will also be renamed to `.jpg`. (This affects only the _generated_ images, _not_ your originals!)

* **Preview**: [This is how the sample page will look like.](http://kaufen-ist-toll.de/demos/mkthumbsf6/sample-gallery/) _(LOTS of documentation to be found there—just below the images!)_
