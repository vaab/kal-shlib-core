

shlibdir = $(libdir)/vlfs

nodist_sysconf_DATA = shlib
dist_shlib_SOURCE = shlib.sources  

shlib: shlib.sources Makefile.am
	cat shlib.sources                                                  | \
	sed "s,%%shlib_path%%,$(shlibdir),g" > shlib

EXTRA_DIST = shlib.sources
DISTCLEANFILES = shlib
