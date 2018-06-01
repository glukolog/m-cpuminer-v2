
if WANT_JANSSON
JANSSON_INCLUDES= -I$(top_srcdir)/compat/jansson
else
JANSSON_INCLUDES=
endif

EXTRA_DIST	= example-cfg.json nomacro.pl

SUBDIRS		= compat m7

INCLUDES	= $(PTHREAD_FLAGS) -fno-strict-aliasing $(JANSSON_INCLUDES)
INCLUDES   += -I$(top_srcdir)/m7

bin_PROGRAMS	= m-minerd

dist_man_MANS	= m-minerd.1

m_minerd_SOURCES	= elist.h miner.h compat.h \
		  cpu-miner.c util.c \
		  sha2.c scrypt.c m7mhash.c
if USE_ASM
if ARCH_x86
m_minerd_SOURCES += sha2-x86.S scrypt-x86.S
endif
if ARCH_x86_64
m_minerd_SOURCES += sha2-x64.S scrypt-x64.S
endif
if ARCH_ARM
m_minerd_SOURCES += sha2-arm.S scrypt-arm.S sha256-armv4.S sha512-armv4.S
endif
if ARCH_aarch64
m_minerd_SOURCES += sha256-armv8-aarch64.S sha512-armv8-aarch64-asm.S
endif
if ARCH_aarch32
m_minerd_SOURCES += sha256-armv8-aarch32.S
endif
endif
m_minerd_LDFLAGS	= $(PTHREAD_FLAGS)  $(LDFLAGS)
m_minerd_LDADD	= @LIBCURL@ @JANSSON_LIBS@ @PTHREAD_LIBS@ @WS2_LIBS@ @M7M_LIBS@ -lgmp -lcurl -lm
m_minerd_CPPFLAGS = -Im7 $(CFLAGS)
