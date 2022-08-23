# exiftool
exiftool is a platform independent tool to read or write exif data from pictures.
this tool works on all major operating systems
[tool webpage]([ExifTool by Phil Harvey](https://exiftool.org/))
[github page](https://github.com/exiftool/exiftool)

>**NOTE:** with normal use, the tool will read the exif data from a picture and dumps it as text, so to process the output, it is customary to use other tools, mainly [[grep]] in linux, or better yet, use it in [[Python]] to do all sort of cool stuff

## Getting Started with exiftool
a normal use case of exiftool is to extract the exif data from an image, we do this simply by calling the tool followed by the picture
`exiftool path_to_image`
this will dump a text containing the exif data from the picture.

