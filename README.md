# sv-swap
sv-swap is a tiny command line utility for changing color properties on svg files.
It's main use is to modify a single style property globally in an svg file. I use this with simple svgs to quickly produce multiple color variants of single line drawings and export to multiple locations. The program can take in multiple hex colors, output destinations, and post fix tags as uix style command options. It can also overwrite the original files as well as generate backups of the original.

tldr: **I use this is a convenience script for working with svgs that are basically just outlines, if you need more than global style value replacement you are welcome to fork this repository and start from there.**
## Installation
- Install or have installed python 3.
- Clone this repository.
- Done!

disclaimer: _I doubt that it works on windows machines_
## Usage

`./sv-swap -c '#000000' -p -f fill doodle.svg`

Overwrites the original file with the fill property set to black. The quotes around the color code are necessary because python reads the `#` as a comment.

`./sv-swap -c '#000000' -p fill doodle.svg`

Throws an error because sv-swap **will not** overwrite files unless the -f option is provided.

`./sv-swap -t black -d black -c '#000000' -p fill doodle.svg`

Does the same as the first *but* appends the file name with `-black`, as well as writes the output file in the directory `./black`. It will create the directory if it does not exist, place the file in the directory if it does exist, but will fail if there is a file occupying that namespace. The end result would be `./black/doodle-black.svg`

`./sv-swap -c '#000000' -p -b -f fill doodle.svg`

Will do the same as the first but also create a backup in the same location as the original with the extension .svg.bak

`./sv-swap -d 'black white red' -c '#000000 #FFFFFF #FF0000' doodle.svg`

Will create three directories, black, red and white, and then change the fill property in that order and place in the respective directories with no tag appended. With multiple colors or output directories the options are matched by the order they are specified. You may output all files to one directory by specifying only one -d parameter, but make sure you specify different -t tags or else it will fail. Likewise you may specify no tag, but output to multiple directories. Fill is the default option for -p. Keep in mind the single quotes are necessary when specifying mulltiple output directories.

`./sv-swap -t 'red white' -c '#000000 #FFFFFF' doodle.svg`

Without specifying a destination directory files will be placed in the location of the original.

`./sv-swap -t 'black white' -c '#000000 #FFFFFF' doodle`

Specifying a directory as a target will iterate through it's contents. Non svg files will be skipped.

`./sv-swap -t 'black white' -c -R '#000000 #FFFFFF' doodle`

-R will recursively read child directories. Does nothing if you specify only a single file. 

`./sv-swap -d 'black white red' -c '#000000 #FFFFFF #FF0000' -t 'black white red' -f -v -b -R origin other`

Creates the three named directories with the three matching colors, tags them with the matching names, overwrite files with the output file names, be verbose, and create backups of everything in the directories origin and other as well as their sub directories.

**Will probably add support for multiple style properties**