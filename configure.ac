#                                               -*- Autoconf -*-
# Process this file with autoconf to produce a configure script.

AC_PREREQ([2.63])
AC_INIT([guile-mathematica], [0.01], [shane.celis@gmail.com])
AC_CONFIG_AUX_DIR([support/build-aux])
# Lies.
#AM_INIT_GUILE_MODULE

# We're going to use GNUMake and we're going to like it.
AM_INIT_AUTOMAKE([-Wall foreign -Wno-portability parallel-tests])
AM_SILENT_RULES([yes])
AC_CONFIG_MACRO_DIR([support/m4])
# Checks for programs.
AC_PROG_CC_C99
AC_PROG_CC_C_O
AC_PROG_LIBTOOL

AC_CHECK_PROG(NOWEB_CHECK,noweb,yes)
if test x"$NOWEB_CHECK" != x"yes" ; then
    AC_MSG_WARN([Must have noweb installed to alter literate source code.])
fi
AC_ARG_ENABLE([noweb],
              [AC_HELP_STRING([--enable-noweb=@<:@yes/no@:>@],
                              [Enable noweb @<:@default=yes@:>@])],
              [enable_noweb=no],
              [enable_noweb=yes])
AM_CONDITIONAL([NOWEB], [test x"$NOWEB_CHECK" = xyes && test x"$enable_noweb" = xyes])

AC_ARG_ENABLE([latexmk],
              [AC_HELP_STRING([--enable-latexmk=@<:@yes/no@:>@],
                              [Enable latexmk @<:@default=yes@:>@])],
              [enable_latexmk=no],
              [enable_latexmk=yes])
AC_CHECK_PROG(LATEXMK_CHECK,latexmk,yes)
if test x"$LATEXMK_CHECK" != x"yes" ; then
    AC_MSG_WARN([Must have latexmk installed to produce PDFs.])
fi
AM_CONDITIONAL([LATEXMK], [test x"$LATEXMK_CHECK" = xyes && test x"$enable_latexmk" = xyes])

GUILE_PROGS

# Checks for libraries.
PKG_CHECK_MODULES([GUILE], [guile-2.0])

if test "$prefix" == "/usr/local"; then
   GUILE_SITE_LIB="$(pkg-config guile-2.0 --variable=pkgdatadir)/site";
else
   GUILE_SITE_LIB="$prefix/share/guile/site";
fi
AC_SUBST(GUILE_SITE_LIB)

AC_SUBST(DISTDIR, ["${PACKAGE_TARNAME}-${PACKAGE_VERSION}"])

#PKG_CHECK_MODULES([EMACSY], [libemacsy])
#AX_CHECK_GLUT
# The autoconf macro does not prefer these frameworks over the
# standard X11 locations.

# Checks for header files.
AC_HEADER_STDC
AC_CHECK_HEADERS([stdio.h])

AC_CHECK_HEADERS([tap/basic.h], [], [])

# Checks for typedefs, structures, and compiler characteristics.

# Checks for library functions.
AC_CHECK_FUNCS([puts])

# 
dnl AC_SUBST(EMACSY_CFLAGS, ['-I${top_srcdir}/../..'])
dnl AC_SUBST(EMACSY_LIBS, ['${top_srcdir}/../../libemacsy.a'])
AC_SUBST(imagesdir, ['${top_srcdir}/support/images'])
AC_SUBST(automakedir, ['${top_srcdir}/support/automake'])

AC_SUBST(MATHLINK_CFLAGS, ['-I/Applications/Mathematica.app/SystemFiles/Links/MathLink/DeveloperKit/MacOSX-x86-64/MathLinkExamples/../CompilerAdditions'])
AC_SUBST(MATHLINK_LIBS, ['-L/Applications/Mathematica.app/SystemFiles/Links/MathLink/DeveloperKit/MacOSX-x86-64/MathLinkExamples/../CompilerAdditions -lMLi3 -lstdc++ -framework Foundation'])

# Output files.
AC_CONFIG_HEADERS([src/config.h])
AC_CONFIG_FILES([ Makefile
                  bin/runtests
                  src/Makefile 
                  src/minimal-cognition/Makefile 
                  tests/Makefile 
                  tests/works-without-noweb.sh
                  tests/print-install.sh
                  ], [chmod +x bin/runtests])
AC_OUTPUT
