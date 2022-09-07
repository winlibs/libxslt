# libxslt

libxslt is the XSLT C parser and toolkit developed for the Gnome project from
[http://xmlsoft.org/XSLT/](http://xmlsoft.org/XSLT/)

PHP currently uses version 1.1.27 released 2012.09.12

# Building for PHP

Due to the way we link libxslt and libxml2, we have our own custom libxslt
build. The change lies in the fact that we dynamically link the static libxslt
lib to the libxml2 library. When libxslt is statically built into an
extension, it dynamically links to the php dll exporting the libxml2 symbols.
In order to support pre Win2K systems, libxslt is built without crypto
support:

    cscript configure.js lib="path to iconv lib dir;path to libxml2 lib dir;" include="path to iconv header dir;path to libxml2 header dir" modules=yes crypto=no vcmanifest=yes

Our custom build requires changes to the Makefile.msvc file. The patch can be found within the
libxslt win32 directory.
