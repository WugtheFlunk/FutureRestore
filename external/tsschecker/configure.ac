AC_PREREQ([2.69])
AC_INIT([tsschecker], [1.0.4], [tihmstar@gmail.com])

# Prepare for automake.
AM_INIT_AUTOMAKE([foreign])
AC_CONFIG_SRCDIR([tsschecker/tsschecker.h])
AC_CONFIG_HEADERS([config.h])

# Checks the platform.
AC_MSG_CHECKING([whether to enable WIN32 specific flags])
case "$host_os" in
*mingw*)
        win32=true
        AC_MSG_RESULT([yes])
	AC_CHECK_TOOL(WINDRES, windres)
  ;;
*)
        win32=false
        AC_MSG_RESULT([no])
  ;;
esac
AM_CONDITIONAL(WIN32, test x$win32 = xtrue)

# Checks for programs.
AC_PROG_CC
CFLAGS+=" -std=c11"
AC_PROG_INSTALL
AC_PROG_LIBTOOL
AC_CONFIG_MACRO_DIRS([m4])

# Versioning.
CFLAGS+=" -D TSSCHECKER_VERSION_COUNT=\\\"$(git rev-list --count HEAD | tr -d '\n')\\\""
CFLAGS+=" -D TSSCHECKER_VERSION_SHA=\\\"$(git rev-parse HEAD | tr -d '\n')\\\""

# Checks for libraries.
AC_CANONICAL_HOST

AC_ARG_WITH(
    [libcrypto],
    [AS_HELP_STRING([--with-libcrypto], [build with libcrypto (default for non-Mac)])],
    [],
    [
        case "${host_os}" in
            darwin*)
                with_libcrypto=no
                ;;
            *)
                with_libcrypto=yes
                ;;
        esac
    ]
)

PKG_CHECK_MODULES(libplist, libplist >= 1.0)
PKG_CHECK_MODULES(libcurl, libcurl >= 1.0)
PKG_CHECK_MODULES(libfragmentzip, libfragmentzip >= 1.0)
AS_IF([test "x$with_libcrypto" != xno],
    [PKG_CHECK_MODULES(libcrypto, libcrypto >= 1.0)]
)
PKG_CHECK_MODULES(libirecovery, libirecovery >= 0.2.0)

# Checks for header files.
AC_CHECK_HEADERS([getopt.h stddef.h stdlib.h string.h stdio.h unistd.h])

# Checks for typedefs, structures, and compiler characteristics.
AC_TYPE_INT32_T
AC_TYPE_INT64_T
AC_TYPE_SIZE_T
AC_TYPE_UINT32_T
AC_TYPE_UINT64_T
AC_TYPE_UINT8_T

# Checks for library functions.
AC_FUNC_ERROR_AT_LINE
AC_FUNC_MALLOC
AC_FUNC_REALLOC
AC_CHECK_FUNCS([memset mkdir pow strchr strdup strstr])

case $CFLAGS in
  *TSSCHECKER_NOMAIN*)
    nomain=true
  ;;
  *)
  ;;
esac

AM_CONDITIONAL(NOMAIN, test x$nomain == xtrue)

AC_CONFIG_FILES([Makefile tsschecker/Makefile])
AC_OUTPUT
