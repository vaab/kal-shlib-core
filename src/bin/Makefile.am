bin_PROGRAMS = shlib

# shlibdir = $(libdir)/vlfs

# nodist_sysconf_DATA = shlib
dist_shlib_SOURCES = shlib.sources

shlib$(EXEEXT): shlib.sources Makefile.am
	cat shlib.sources | \
	sed "s,%%sysconfdir%%,$(sysconfdir),g" > shlib$(EXEEXT)

EXTRA_DIST = shlib.sources
DISTCLEANFILES = shlib
