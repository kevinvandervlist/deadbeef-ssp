# bin_PROGRAMS = ssp.so
pkglibdir = $(PLUGIN_INST)
pkglib_LTLIBRARIES = libssp.la
libssp_la_SOURCES = ssp.c
libssp_la_LDFLAGS = -module $(HAVE_DBUS_LIBS) $(GLIB2_LIBS) $(DBUS_GLIB_1_LIBS)

libssp_la_LIBADD = $(LDADD)
AM_CFLAGS = $(HAVE_DBUS_CFLAGS) $(GLIB2_CFLAGS) $(DBUS_GLIB_1_CFLAGS) -std=c99 -fPIC -DPIC
