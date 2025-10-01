> [!IMPORTANT]
> This specification is purely conceptual at the moment, and no tools exist to use this specification.

# MSVG v0.0
## Overview
Minecraft Scalable Vector Graphics (MSVG) is a modified specification of [SVG](https://www.w3.org/TR/SVG2/) intended to be used for a hypothetical Minecraft mod that would allow for vector graphics to be used for textures.

MSVG has two key differences from SVG:
1. The formatting has been compacted to be as preformant as possible; performance is prioritized over human readability.
2. Features/components that aren't essential for the goal of MSVG have been removed.

## Header
The header must precede any other data in the `.msvg` file, and should be formatted as follows:

```
File identifier      "MSVG"
Viewbox              $XX YY WW HH
Flags                %x0000000
File Length          $xxxxx
```

The first four bytes of a `.msvg` file should be `4D 53 56 47`, or "MSVG" using UTF-8 text encoding. This is to ensure that no misnamed files can be used.

The next four bytes are the viewbox sizing definitions. The first two bytes represent the viewbox's top left x and y coordinates, while the last two bytes represent the width and height.

Next, one byte is used to signify the rendering type used for the texture

After that, one byte is dedicated to MSVG flags, which are covered in more detail in the next section.

The final five bytes declare the size of the file, with a maximum of 0xFFFFF (1048575 bytes). (Anything over this limit is beyond the scope of reason and if for some esoteric reason you need more, you can modify this limit yourself in any implementation.)
### Header Flags
The first bit of the flag byte controls whether the msvg should be treated as transparent or use a fallback color as the background.

No other bits are currently used in the flag byte.
