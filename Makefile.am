AM_MAKEFLAGS = --no-print-directory

include_HEADERS =

AM_CFLAGS = $(WARNING_CFLAGS) $(BUILD_CFLAGS) @GLIB_CFLAGS@
AM_LDFLAGS = $(BUILD_LDFLAGS)

libexec_PROGRAMS = src/knotd tools/ktool

src_knotd_SOURCES = src/main.c \
			src/manager.h src/manager.c \
			src/proto.h src/node.h \
			src/http.h src/http.c \
			src/unix.c

src_knotd_LDADD = @GLIB_LIBS@
src_knotd_LDFLAGS = $(AM_LDFLAGS)
src_knotd_CFLAGS = $(AM_CFLAGS)

tools_ktool_SOURCES = tools/ktool.c
tools_ktool_LDADD = @GLIB_LIBS@
tools_ktool_LDFLAGS = $(AM_LDFLAGS)
tools_ktool_CFLAGS = $(AM_CFLAGS)

DISTCLEANFILES =

MAINTAINERCLEANFILES = Makefile.in \
	aclocal.m4 configure config.h.in config.sub config.guess \
	ltmain.sh depcomp compile missing install-sh

clean-local:
	$(RM) -r src/knotd tools/ktool