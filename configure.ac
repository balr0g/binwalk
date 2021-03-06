AC_PREREQ([2.65])
AC_INIT()

AC_PROG_CC
AC_LANG(C)

AC_TYPE_SIZE_T
AC_FUNC_MALLOC

AC_ARG_WITH([python],
            [AS_HELP_STRING([--with-python=python], [explicitly install using the specified python interpreter (python2, python3, etc)])],
            [PYTHON=$withval],
            [PYTHON=python])

AC_ARG_ENABLE([clibs],
              [AS_HELP_STRING([--disable-clibs], [do not build/install dependent c libraries])],
              [BUILD_C_LIBS=0],
              [BUILD_C_LIBS=1])

AC_ARG_ENABLE([libmagic],
              [AS_HELP_STRING([--disable-libmagic], [do not build/install the bundled libmagic library])],
              [BUILD_MAGIC=0],
              [BUILD_MAGIC=1])

AC_ARG_ENABLE([libfuzzy],
              [AS_HELP_STRING([--disable-libfuzzy], [do not build/install the bundled libfuzzy library])],
              [BUILD_FUZZY=0],
              [BUILD_FUZZY=1])

CFLAGS="-Wall -fPIC $CFLAGS"
INSTALL_OPTIONS="-m644"

if test "$(uname)" == "Darwin"
then
	SONAME="-install_name"
	SOEXT="dylib"
else
	SONAME="-soname"
	SOEXT="so"
fi

if test "$BUILD_C_LIBS" != "0"
then
    if test "$BUILD_MAGIC" != "0"
    then
        (cd ./src/C/file-*/ && autoreconf -v && ./configure) || exit 1
    fi

    if test "$BUILD_FUZZY" != "0"
    then
        (cd ./src/C/ssdeep-*/ && autoreconf -v && ./configure) || exit 1
    fi
fi

AC_SUBST(BUILD_C_LIBS, $BUILD_C_LIBS)
AC_SUBST(BUILD_MAGIC, $BUILD_MAGIC)
AC_SUBST(BUILD_FUZZY, $BUILD_FUZZY)
AC_SUBST(PYTHON, $PYTHON)
AC_SUBST(SONAME, $SONAME)
AC_SUBST(SOEXT, $SOEXT)
AC_SUBST(PLATFORM, $(uname -s))
AC_SUBST(INSTALL_OPTIONS, $INSTALL_OPTIONS)
AC_CONFIG_FILES([Makefile])
AC_OUTPUT
