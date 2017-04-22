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

### Standalone

If run within a »normal« image folder, _makethumbsf6_ will also generate a **HTML sample file** with a **[PhotoSwipe](http://photoswipe.com/) lightbox** and almost all **documentation included**.

_You can use this to copy-and-paste actual responsive images and markup code for your website, or just for creating a nice slide show on the fly._

### ZURB Foundation 6 Frontend Framework

If run inside a **[ZURB Foundation 6](http://foundation.zurb.com/)** folder structure (i.e, something like `src/assets/img/gallery/album-01/…`), it will instead generate a **ready-to-run partial** inside your `src/partials` folder. You can simply include this partial on a gallery page using Panini, for example as `{{> gallery-gallery-album-01 gid=1}}`.

_You typically use this when working on projects using the Foundation framework, but the generated markup can easily be adapted for other frameworks._

### Automatic headlines, image captions and markup comments

I strongly believe that image information should be stored together with the image (much like we do it with FLAC or MP3 files already). The image files can then be copied, moved, put on the web without the need of updating databases, changing HTML markup manually, and even the image credits will still be in place if someone downloads it.

Like image and new agencies already do for a long time, I encourage you to store data like a headline, a caption text, the photographer’s name and a copyright notice _inside_ your images. You can use tools like _exiftool_ (or many others) for that, or Adobe Photoshop, Adobe Lightroom, even Windows’ image properties or Mac OSX’ finder.

_Makethumbsf6_ will then _automatically_ read this data, and present you with a beautiful and customizable view. It’ll even generate _map links_ for you, if the GPS location is stored in the images (like many new cameras and smartphones do).

Additionally, _makethumbsf6_ will automatically put the photographer’s name and (if specified) additional image credits (like maybe the image agency’s name) next to your caption text. This makes it super-easy for you to follow licensing or local laws, if so required.

**Run _makethumbsf6_ inside the `sample-gallery` folder, then view the generated HTML file with your browser.** All sample images have tags (some even GPS data) so you can get a first idea of what can be done. Feel free to change some tags within the sample images (maybe using _exiftool_ or another application you prefer), then run _makethumbsf6_ again to see what’s changed.

## Customization: Have _makethumbsf6_ do what _you_ need!

My script is highly customizable and each option very well documented. Just make a backup, then open the `makethumbsf6` script with a normal (UTF-8-capable) text editor and have a peek inside.

You’ll find a lot of customization options that you can change to fit _your_ needs. Here are just a very few:

* **USE_SQUARE_THUMBS**: Use square thumbnails (auto-cropped), or »normal« ones (having the same aspect ratio as the original image)?

* **USE_LIGHTBOX**: For the stanbalone version, include the _PhotoSwipe_ lightbox?

* **FIGURE_TITLE**: Force the same title for all thumbnails (i.e., »Click to magnify« instead of the image’s headline)?

* **IMAGE_LINKTO**: Link to the original image or to some defined (max.) size like "xl"?

* **USE_DATE, DATEFORMAT, DATE_LEADOUT**: Define if the »image taken on« date should be shown, and in which format.

* **CREDITS_LEADIN, CREDITS_LEADOUT**: Put some nice text around the image credits (i.e. »(Photo: Photographer / Agency)« instead of »Photographer / Agency«)?

* **USE_MAPS, MAPLINK_TEXT**: Use map links if image has GPS data? What text to display?

* **F_NAME, F_BREAKPOINT, F_CONV**: Number and names of different image versions to generate, their (or your framework’s) responsive breakpoints, and even the commands for each resolution to be given to ImageMagick’s `convert`.

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

* A _Linux-type OS_ that has a _bash_ shell with array support and can do 'sort -z'.
* [ImageMagick](https://www.imagemagick.org/)
* [Exiftool](http://www.sno.phy.queensu.ca/~phil/exiftool/)

* For changes and setting options: A text editor that handles UTF-8 (no BOM please).
