MKDIR=mkdir
CP=cp
GIT=git
ZIP=zip
FIND=find

KNOT_SERVICE_DOWNLOAD_DIR = download

AM_MAKEFLAGS = --no-print-directory

include_HEADERS =
modules_sources =
modules_ldadd =
modules_cflags =
INCLUDES =

AM_CFLAGS = $(WARNING_CFLAGS) $(BUILD_CFLAGS) @GLIB_CFLAGS@
AM_LDFLAGS = $(BUILD_LDFLAGS)

bin_PROGRAMS = src/knotd
noinst_PROGRAMS = tools/ktool unit/ktest

include Makefile.modules

src_knotd_SOURCES = src/main.c \
			src/manager.h src/manager.c \
			src/msg.c src/msg.h \
			src/proto.h src/node.h \
			src/log.h \
			$(modules_sources)

src_knotd_LDADD = @GLIB_LIBS@ $(modules_ldadd) -lm
src_knotd_LDFLAGS = $(AM_LDFLAGS)
src_knotd_CFLAGS = $(AM_CFLAGS) $(modules_cflags)

tools_ktool_SOURCES = tools/ktool.c
tools_ktool_LDADD = @GLIB_LIBS@ @JSON_LIBS@
tools_ktool_LDFLAGS = $(AM_LDFLAGS)
tools_ktool_CFLAGS = $(AM_CFLAGS) @JSON_CFLAGS@

unit_ktest_SOURCES = unit/ktest.c 			\
			src/log.h

unit_ktest_LDADD = @GLIB_LIBS@
unit_ktest_LDFLAGS = $(AM_LDFLAGS)
unit_ktest_CFLAGS = $(AM_CFLAGS) @GLIB_CFLAGS@

DISTCLEANFILES =

MAINTAINERCLEANFILES = Makefile.in \
	aclocal.m4 configure config.h.in config.sub config.guess \
	ltmain.sh depcomp compile missing install-sh

KNOT_HAL_LIB_VERSION = master
KNOT_HAL_LIB_REPO = knot-hal-source
KNOT_HAL_LIB_SITE = https://github.com/CESARBR/$(KNOT_HAL_LIB_REPO).git
KNOT_HAL_HDR_LIB_DIR = ./$(KNOT_SERVICE_DOWNLOAD_DIR)/$(KNOT_HAL_LIB_REPO)/include
KNOT_HAL_SRC_LIB_DIR = ./$(KNOT_SERVICE_DOWNLOAD_DIR)/$(KNOT_HAL_LIB_REPO)/src/hal

default: all

all:  $(KNOT_HAL_TARGET)

$(KNOT_SERVICE_DOWNLOAD_DIR):
	$(MKDIR) -p ./$(KNOT_SERVICE_DOWNLOAD_DIR)

$(KNOT_HAL_LIB_DIR):  $(KNOT_SERVICE_DOWNLOAD_DIR)
	$(GIT) clone -b $(KNOT_HAL_LIB_VERSION) $(KNOT_HAL_LIB_SITE) ./$(KNOT_SERVICE_DOWNLOAD_DIR)/$(KNOT_HAL_LIB_REPO)

$(KNOT_THING_TARGET):  $(KNOT_HAL_LIB_DIR)
	$(MKDIR) -p ./$(KNOT_SERVICE_DOWNLOAD_DIR)/src/log

	$(CP) -r $(KNOT_HAL_HDR_LIB_DIR)/avr_log.h ./$(KNOT_SERVICE_DOWNLOAD_DIR)/src/log

	$(CP) -r ./$(KNOT_HAL_SRC_LIB_DIR)/log/log_avr.cpp ./$(KNOT_SERVICE_DOWNLOAD_DIR)/src/log

clean-local:
	$(RM) -r src/knotd tools/ktool unit/ktest
