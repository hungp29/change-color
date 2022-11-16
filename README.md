# change-color

### ARGB Memory Representation

The format used in Image Processing example is a version of the RGB family called ARGB, where A stands for alpha (transparency).

The representation of this color in memory is as follows:

    ---------------------------------
    | Byte 3| Byte 2| Byte 1| Byte 0|
    ---------------------------------
    | ALPHA |  RED  | GREEN |  BLUE |
    ---------------------------------

As we can see, each component is represented by a single byte (8 bits), so the value of each component is between 0 (0x in hexadecimal) and 255. (0xFF in hexadecimal).
Because we have 4 bytes, we can store the entire color of a pixel in a 'int' variable.

### Extraction color from RGB
To obtain a specific component (red, green, or blue), we must first remove all other color components from the pixel while retaining the desired component.

We use a bitmask to accomplish this.

A bitmask specifies which bits should be kept and which should be cleared.

To remove a component, we use a bitwise AND with 0x00 (0000 0000 in binary) because X AND 0 = 0, for any X.

To keep the value of a component, we use a bitwise AND with 0xFF (1111 1111 in binary) because X AND 1 = X for any X.

Using the >> operator, we must shift all of the bits in the bitmask result to the right.

- We don't need to shift for the blue color extraction because it's already the right-most byte.

- To extract the green color, we must shift all of the bits 1 byte (8 bits) to the right.

- To extract the red color, we must shift all of the bits 2 bytes (16 bits) to the right.

### Combining Color

We do the inverse of color component extraction. We take each component and move it to the appropriate location in the ARGB pixel representation.

- Because blue is the least significant byte, we simply bitwise OR the pixel color representation with the blue component.

- Green must be placed in the second byte, so it is shifted one byte (8 bits) to the left before being bitwise ORed with the pixel color.

- Similarly, red must be placed at the third byte so that its component is shifted 2 bytes (16 bits) to the left before being bitwise ORed with the pixel color.

