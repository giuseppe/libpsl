# suffixes.c must be created before psl.c is compiled
BUILT_SOURCES = suffixes.c

# suffixes.c is a built source that must be cleaned
CLEANFILES = suffixes.c

lib_LTLIBRARIES = libpsl.la

libpsl_la_SOURCES = psl.c
libpsl_la_CPPFLAGS = -I$(top_srcdir)/include
# include ABI version information
libpsl_la_LDFLAGS = -version-info $(LIBPSL_SO_VERSION)
if WITH_LIBICU
  libpsl_la_LDFLAGS += -licuuc
endif
if WITH_LIBIDN2
  libpsl_la_LDFLAGS += -lidn2 -lunistring
endif
if WITH_LIBIDN
  libpsl_la_LDFLAGS += -lidn -lunistring
endif

noinst_PROGRAMS = psl2c
psl2c_SOURCES = psl2c.c
psl2c_CPPFLAGS = -I$(top_srcdir)/include -D _GNU_SOURCE
if BUILTIN_GENERATOR_LIBICU
  psl2c_LDADD = -licuuc
endif
if BUILTIN_GENERATOR_LIBIDN2
  psl2c_LDADD = @LTLIBICONV@ -lidn2 -lunistring
endif
if BUILTIN_GENERATOR_LIBIDN
  psl2c_LDADD = @LTLIBICONV@ -lidn -lunistring
endif

# Build rule for suffix.c
# PSL_FILE can be set by ./configure --with-psl-file=[PATH]
suffixes.c: $(PSL_FILE) psl2c$(EXEEXT)
	./psl2c$(EXEEXT) "$(PSL_FILE)" suffixes.c
