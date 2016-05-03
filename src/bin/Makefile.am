bin_PROGRAMS = shlib bash-shlib

# nodist_sysconf_DATA = shlib
dist_shlib_SOURCES = shlib.sources
dist_bash_shlib_SOURCES = bash-shlib

shlib$(EXEEXT): shlib.sources Makefile.am
	cat shlib.sources | \
	sed "s,%%sysconfdir%%,$(sysconfdir),g" > shlib$(EXEEXT)

EXTRA_DIST = shlib.sources bash-shlib
DISTCLEANFILES = shlib
