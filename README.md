# img2rom_converter
Generates hardware ROM in VHDL from picture file

## Description

Usage: 

    pic2rom INPUTFILE OUTPUTFILE ENTITY R\_WL G\_WL B\_WL

Creates the file OUTPUTFILE containing the VHDL description of a ROM
initialized from INPUTFILE image content.

The generated ROM, named ENTITY has SIZE\_X * SIZE\_Y elements of
R\_WL+G\_WL+B\_WL bits with SIZE\_X and SIZE\_Y the source image
pixels dimensions.

ROM[ADDR] contains the value of pixel X,Y such as :
ADDR = Y*SIZE_X + X.
Each pixel color value C is coded on R\_WL+G\_WL+B\_WL bits with the
following format :

    C[R_WL+G_WL+B_WL-1 .. G_WL+B_WL] = red component value (R_WL bits)
    C[     G_WL+B_WL-1 ..      B_WL] = green component value (G_WL bits)
    C[          B_WL-1 ..         0] = blue component value (B_WL bits)

Example: 

    pic2rom kodim23\_edited.png rom\_img.vhd rom_img 5 6 5

## BUGS
 * Colors are washed out, even after adjusting gamma
   (maybe only when used to display on Terasic LT24)

## LIMITATIONS :
 * Tested only with 8 bits per channel (with RGB png file)
 * Color indexed images are currently unsupported 
 * Only color images are currently supported (b&w image would produce
   only one channel)
 * Requires r\_wl+g\_wl+b\_wl <= 64
 * If r\_wl+g\_wl+b\_wl != 16, needs to update fprintf format in source code
 * if x*y > 99999 fprintf format should be updated in source code (only for
   generated VHDL code alignment, not really necessary)

## Requirements

 * GNU/Octave and the "image" package.
 * pic2rom function should be compatible with Matlab (not tested)

