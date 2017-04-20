# makethumbsf6

## Make thumbnails, responsive images and HTML/Zurb Foundation 6 markup all in one go!

A _bash_ script, put it in `~/bin`, `chmod +x makethumbsf6` and for a first (standalone) try run it from _inside_ the `sample-gallery` folder.

It should create a set of subfolders:

* `t` — thumbnails, original aspect ratio
* `ts` — squared & cropped thumbnails, 120x120px
* `s` — responsive images for small screens (320w)
* `m` — responsive images for medium screens (640w)
* `l` — resonsive images for large screens (1024w)
* `xl` — responsive images for extra-large screens (1920w)
  
It’ll also generate a HTML sample file with a lightbox and almost all documentation included.

You might want to peek at the code—makethumbsf6 is very well documented and has a lot of customization settings.

More documentation will follow.
