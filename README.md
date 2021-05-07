# ImageSize
Command line image sizer and cropper.

# Version
- v1.3
- May 7, 2021
- macOS, Linux, Windows
- [MIT License](LICENSE)
- By Abe Pralle
- [github.com/AbePralle/ImageSize](https://github.com/AbePralle/ImageSize)

# Installation

## Windows and macOS

Download precompiled binaries for Windows and macOS from the [Releases](https://github.com/AbePralle/ImageSize/releases/) page.

# Building From Source
1. Install [Rogue](https://github.com/AbePralle/Rogue).
2. Run `rogo` in the root folder of this repo.

# Usage

```
USAGE
  imagesize [input-patterns] [actions] [replace | output filepath]

INPUT PATTERNS
  path/to/file, *.png, "**/*.jpg"

ACTIONS
  anchor [HxV]
  anchor [left | right | top | bottom | center]
    Changes anchor for successive 'crop' and 'aspect' commands. 0.5x0.5/'center' by default.
      'anchor 0x0'     == 'anchor top left' == 'anchor left top'
      'anchor 0.5x0'   == 'anchor top'
      'anchor 0.5x0.5' == 'anchor center'
      'anchor 1x1'     == 'anchor bottom right'

  aspect-fill WxH
  aspect-fit  WxH
    Crops to fill or fit an aspect ratio. 'aspect-fill 1024x768' equivalent to 'aspect-fill 4x3'.
    Uses current 'anchor' point or 'center' by default.

  crop [WxH | Wx | xH]
    Crops/expands image using current 'anchor' point (default: 'center').

  flip | hflip | vflip
    Flips (mirrors) an image horizontally or vertically. 'flip' == 'hflip'.

  output <filepath>
    Designates output folder, filename, or format - use 'replace' instead of 'output' to replace
    original files with the modified versions. Output filepaths can contain the following
    placeholders which are replaced on save:
      {path}     - The original path without the filename.
      {filename} - The original filename+extension without the path.
      {name}     - The original filename without the path or extension.
      {ext}      - The extension of the original filename.
      {001}      - Sequence specification. '{001}' writes '001', '002', etc.
      {w}, {h}   - The width or height of the output image.

  replace
    Indicates that the original file should be replaced with the result.

  resize  [WxH | Wx | xH]
    'resize 1024x' on a 512x200 image would create a 1024x400 image, etc.

  reshape WxH
    Performs an `aspect-fill` followed by a `resize`.

  rotate [cw|ccw|180]
    Rotates the image 90 degrees clockwise, 90 degrees counter-clockwise, or 180 degrees.

  splice [h | v | WxH | Wx | xH]
    Joins all images together into a single horizontal row (`h`), vertical column (`v`), or grid.

  split WxH
    Splits apart each image into "WxH" individual images. "W" and "H" are column and row counts, not
    pixel sizes.

EXAMPLES
  # Print the image size of every JPG.
  imagesize *.jpg

  # Create a 320x200 JPG thumbnail of each PNG image.
  imagesize *.png aspect-fill 4x3 resize 320x200 output "Thumbnails/{name}.jpg"

  # A shorter equivalent to the above.
  imagesize *.png reshape 320x200 output "Thumbnails/{name}.jpg"

  # Rotate an image 90º counter-clockwise and replace the original.
  imagesize WrongOrientation.png rotate ccw replace

  # Splice together a horizontal strip of images.
  imagesize *.png splice h

  # Arrange images into a grid that's 2 rows high.
  imagesize *.png splice x2

  # Split a 600x600 image containing 3x2 tiles into six 300x200 tiles "Tile-0.jpg".."Tile-5.jpg".
  imagesize Tiles.png split 3x2 output "Tile-{0}.jpg"
```

