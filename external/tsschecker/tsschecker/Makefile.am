AM_CFLAGS = $(libplist_CFLAGS) $(libfragmentzip_CFLAGS) $(libcurl_CFLAGS) $(libcrypto_CFLAGS) $(libirecovery_CFLAGS)  -I$(top_srcdir)/external/jssy/jssy/
AM_LDFLAGS = $(libplist_LIBS) $(libfragmentzip_LIBS) $(libcurl_LIBS) $(libcrypto_LIBS) $(libirecovery_LIBS) -lm

lib_LIBRARIES = libjssy.a
libjssy_a_CFLAGS = $(AM_CFLAGS)
libjssy_a_SOURCES = $(top_srcdir)/external/jssy/jssy/jssy.c

if NOMAIN
noinst_LTLIBRARIES = libtsschecker.la
libtsschecker_la_SOURCES = tsschecker.c tss.c download.c
libtsschecker_la_CFLAGS = $(AM_CFLAGS)
libtsschecker_la_LIBADD = $(AM_LDFLAGS) libjssy.a
else
bin_PROGRAMS = tsschecker
tsschecker_CFLAGS = $(AM_CFLAGS)
tsschecker_LDADD = $(AM_LDFLAGS) libjssy.a

if WIN32
tsschecker_LDFLAGS = -all-static -static-libgcc
endif

tsschecker_SOURCES = tsschecker.c tss.c download.c main.c
endif
