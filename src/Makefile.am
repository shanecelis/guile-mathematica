SUBDIRS = 

MAINTAINERCLEANFILES = Makefile.in config.h.in 

# Stop make from deleting intermediate files. 
# http://darrendev.blogspot.com/2008/06/stopping-make-delete-intermediate-files.html
.SECONDARY:

NOWEB_DOCS = mathematica-paper.pdf 
EXTRA_DIST = $(NOWEB_DOCS)

NOWEB_FILES = mathematica.nw
NOWEB_PRODUCTS = mathematica.c mathematica.scm mathematica-test.scm mathematica.h
BUILT_SOURCES = mathematica.c.x
CLEANFILES = $(BUILT_SOURCES)

doc: $(NOWEB_DOCS)

if LATEXMK
all-local : $(NOWEB_DOCS)
CLEANFILES += $(NOWEB_DOCS)

endif

#MARKUP_FLAGS = -markup "$(top_srcdir)/bin/namespace-markup.pl -n ctrnn-appendix=ctrnn -n ctrnn-cat=ctrnn --"
#MARKUP_FLAGS = -markup "$(top_srcdir)/bin/namespace-markup.pl --"
WARN_NOTANGLE_FLAGS = -W 
NOWEAVE_FLAGS = $(MARKUP_FLAGS)
NOTANGLE_C_FLAGS = -c -L $(MARKUP_FLAGS)
NOTANGLE_H_FLAGS = -L $(MARKUP_FLAGS)
lib_LTLIBRARIES = libguile-mathematica.la

AM_CFLAGS = $(GUILE_CFLAGS) $(MATHLINK_CFLAGS) 
libguile_mathematica_la_LIBADD  = $(MATHLINK_LIBS) $(GUILE_LIBS)
libguile_mathematica_la_SOURCES = mathematica.c

check_PROGRAMS = test-links

test_links_LDADD = libguile-mathematica.la
#test_links_LDFLAGS =  $(GUILE_LIBS) $(MATHLINK_LIBS)
test_links_LDFLAGS = $(GUILE_LIBS)
test_links_SOURCES = test-links.c


guilemoduledir = $(GUILE_SITE_LIB)
dist_guilemodule_DATA = mathematica.scm

#TESTS_ENVIRONMENT = $(GUILE) -L $(top_builddir)/src -L $(top_srcdir)/support/scheme -x $(libdir)
#TESTS_ENVIRONMENT = LOG_COMPILER
AM_TESTS_ENVIRONMENT = DYLD_LIBRARY_PATH='$(top_builddir)/src/.libs'; export DYLD_LIBRARY_PATH;
TESTS = plus-test.scm mathematica-test.scm test-links
TEST_EXTENSIONS = .scm 
SCM_LOG_COMPILER = $(top_builddir)/bin/runtests

#LOG_COMPILER = DYLD_LIBRARY_PATH=.: 

# TESTS_ENVIRONMENT = 
# TESTS =  ctrnn-test vision-test 

include $(top_srcdir)/support/automake/noweb.am
include $(top_srcdir)/support/automake/guile.am

mathematica.c.x : mathematica.c
dist-hook:
	cp $(distdir)/*.pdf $(top_distdir)



