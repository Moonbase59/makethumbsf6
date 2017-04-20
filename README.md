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

It’ll also generate a **HTML sample file** with a **[PhotoSwipe](http://photoswipe.com/) lightbox** and almost all **documentation included**.

You might want to peek at the code—makethumbsf6 is very well documented and has a lot of customization settings.

_Hint:_ For performance reasons, _makethumbsf6_ will skip already-made thumbnails and lower-res images when it is run again. If you want to _force_ it, just delete the above-mentioned subfolders.

More documentation will follow. Meanwhile, have fun reading the sample HTML file. ;-)

_The script (makethumbsf6) is MIT licensed, the images in the sample gallery are NOT (though many of them are CC0). Please check the image data and/or the generated HTML code which will show the copyright notices. **Thank you.**_

Drop me a line [@Moonbase59](https://twitter.com/intent/tweet?text=%40Moonbase59&amp;hashtags=makethumbsf6) and let me know what you think. Or [let others know, too](https://twitter.com/intent/tweet?text=Easily%20make%20thumbs%2C%20responsive%20images%2C%20HTML%20markup&url=https%3A%2F%2Fgithub.com%2FMoonbase59%2Fmakethumbsf6&via=Moonbase59&hashtags=makethumbsf6,thumbnails,responsive,foundation)!

## Requirements

* A _Linux-type OS_ that has a _bash_ shell with array support and can do 'sort -z'.
* [ImageMagick](https://www.imagemagick.org/)
* [Exiftool](http://www.sno.phy.queensu.ca/~phil/exiftool/)

* For changes and setting options: A text editor that handles UTF-8 (no BOM please).
