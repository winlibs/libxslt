# libxslt

libxslt is an XSLT processor based on libxml2.

Official releases can be downloaded from
<https://download.gnome.org/sources/libxslt/>

The git repository is hosted on GNOME's GitLab server:
<https://gitlab.gnome.org/GNOME/libxslt>

Bugs should be reported at
<https://gitlab.gnome.org/GNOME/libxslt/-/issues>

Documentation is available at
<https://gitlab.gnome.org/GNOME/libxslt/-/wikis>

The build system is similar to libxml2. Refer to libxml2's README for
build instructions.

# Building for PHP

PHP currently uses version 1.1.45 released 2025.11.30

Due to the way we link libxslt and libxml2, we have our own custom libxslt
build. The change lies in the fact that we dynamically link the static libxslt
lib to the libxml2 library. When libxslt is statically built into an
extension, it dynamically links to the php dll exporting the libxml2 symbols.
In order to support pre Win2K systems, libxslt is built without crypto
support:

    cscript configure.js lib="path to iconv lib dir;path to libxml2 lib dir;" include="path to iconv header dir;path to libxml2 header dir" modules=yes crypto=no vcmanifest=yes

Our custom build requires changes to the Makefile.msvc file. The patch can be found within the
libxslt win32 directory.
