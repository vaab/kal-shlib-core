bin_PROGRAMS = shlib

# shlibdir = $(libdir)/vlfs

# nodist_sysconf_DATA = shlib
dist_shlib_SOURCES = shlib.sources  

shlib: shlib.sources Makefile.am
	cat shlib.sources                                                  | \
	sed "s,%%sysconfdir%%,$(sysconfdir),g" > shlib

EXTRA_DIST = shlib.sources
DISTCLEANFILES = shlib
