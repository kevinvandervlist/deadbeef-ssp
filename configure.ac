dnl Autoconfigure template for DeaDBeeF-ssp, a plugin
dnl written by Kevin van der Vlist. 
dnl http://code.google.com/p/deadbeef-ssp

dnl Autoconf macros:
dnl Initialize autoconf. name, version no, bug report addr
AC_INIT([ssp], [0.1], [kevin@kevinvandervlist.nl])
dnl Autoconf version check:
AC_PREREQ([2.50])
dnl Clean auxilary directory:
AC_CONFIG_AUX_DIR([build-aux])
dnl Path check:
AC_CONFIG_SRCDIR([src/ssp.c])
dnl Libtool:
AC_CONFIG_MACRO_DIR([m4])
dnl Init automake. Turn on all warnings and report 
AM_INIT_AUTOMAKE([foreign -Wall -Werror])
dnl Initialize libtool
LT_INIT
dnl Check for a C compiler. 
AC_PROG_CC
dnl config.h becomes the output header. 
AC_CONFIG_HEADERS([config.h])

dnl Dependencies check:
dnl GLIB:
PKG_CHECK_MODULES([GLIB2], [glib-2.0 dbus-glib-1], GLIB2_CHECK=yes, GLIB2_CHECK=no)

if test "x$GLIB2_CHECK" = "xyes"; then
   dnl Define HAVE_GLIB for the source
   AC_SUBST(GLIB2_CFLAGS)
   AC_SUBST(GLIB2_LIBS)
   AC_CHECK_LIB([glib-2.0], [g_main_loop_new])
   dnl and dbus-glib-1
   PKG_CHECK_MODULES([DBUS_GLIB_1], [dbus-glib-1], DBUS_GLIB_BINDING=yes, DBUS_GLIB_BINDING=no)
   if test "x$DBUS_GLIB_BINDING" = "xno"; then
      AC_ERROR([glib-2.0 found, but no dbus bindings.])
   fi
   AC_SUBST(DBUS_GLIB_1_CFLAGS)
   AC_SUBST(DBUS_GLIB_1_LIBS)
   AC_MSG_NOTICE([Using hook in glib's main-loop]) 
   dnl Dirty hack. Doesnt include pthreads
   AC_CHECK_LIB([pthread], [pthread_create_nonexistent])
   AC_DEFINE([HAVE_LIBPTHREAD], [0])
fi
if test "x$GLIB2_CHECK" = "xno"; then
   dnl Disabled GLIB, use custom polling provided via pthreads.
   AC_MSG_NOTICE([Using pthread'd poller]) 
   AC_CHECK_HEADERS(unistd.h)
   AC_CHECK_HEADERS([pthread.h])
   AC_CHECK_LIB([pthread], [pthread_create])
fi

dnl DBUS:
PKG_CHECK_MODULES(HAVE_DBUS, dbus-1)
AC_SUBST(HAVE_DBUS_CFLAGS)
AC_SUBST(HAVE_DBUS_LIBS)

dnl Install settings: - Thanks bwtari
dnl Search for deadbeef installation directory
AC_PREFIX_PROGRAM(deadbeef)
if test "x$prefix" != xNone; then
    PLUGIN_INST="$prefix/lib/deadbeef"
else
    dnl Use default if nothing is found:
    PLUGIN_INST="$ac_default_prefix/lib/deadbeef"
fi
AC_SUBST(PLUGIN_INST)

dnl Declare the makefiles. 
AC_CONFIG_FILES([Makefile src/Makefile])
dnl Output all files declared above. 
AC_OUTPUT