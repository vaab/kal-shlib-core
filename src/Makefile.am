
# dist_bin_SCRIPTS = $(srcdir)/bin/*


shlibdir = $(libdir)/shlib
#dist_shlib_DATA = $(srcdir)/lib/*

#sysconf_DATA = $(srcdir)/etc/shlib
#shlib_SOURCE = $(srcdir)/etc/shlib.in  


EXTRA_DIST = $(dist_shlib_DATA)

#distcleancheck:
#	@:

distcleancheck_listfiles = \
  find -type f -exec sh -c 'test -f $(scrdir)/{} || echo {}'

SUBDIRS = etc bin
