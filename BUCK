genrule(
  name = 'make',
  out = 'out',
  srcs = glob([
    'source/**/*.h',
    'source/**/*.c',
    'source/**/*.cpp',
    'source/**/*.cnv',
    'source/**/*.icu',
    'source/**/*.in',
    'source/**/*.mak',
    'source/**/*.mk',
    'source/**/*.m4',
    'source/**/*.nrm',
    'source/**/*.res',
    'source/**/*.sed',
    'source/**/*.txt',
    'source/**/*.ucm',
    'source/**/*.xml',
    'source/config/mh-*',
    'source/config/icu-*',
    'source/config.guess',
    'source/config.sub',
    'source/configure',
    'source/install-sh',
    'source/mkinstalldirs',
    'source/runConfigureICU',
  ], excludes = glob([
    'source/samples/**/*.h',
    'source/samples/**/*.cpp',
    'source/samples/**/*.c',
    'source/samples/**/*.txt',
    'source/samples/*/**/*.in',
  ])),
  cmd =
    'platform=\$(case $(uname) in ' +
        '("Linux") ' +
        '  echo "Linux" ' +
        ';; ' +
        '("Darwin") ' +
        '  echo "MacOSX" ' +
        ';; ' +
        '(*) ' +
        '  echo "Unknown" ' +
        ';; ' +
    'esac); ' +
    'cp -r $SRCDIR $OUT && ' +
    'mkdir -p $OUT/source/samples/cal/ && ' +
    'cp $(location //source/samples/cal:Makefile.in) $OUT/source/samples/cal/Makefile.in && ' +
    'mkdir -p $OUT/source/samples/date/ && ' +
    'cp $(location //source/samples/date:Makefile.in) $OUT/source/samples/date/Makefile.in && ' +
    'mkdir -p $OUT/source/samples/layout/ && ' +
    'cp $(location //source/samples/layout:Makefile.in) $OUT/source/samples/layout/Makefile.in && ' +
    'chmod +x $OUT/source/runConfigureICU && ' +
    'chmod +x $OUT/source/configure && ' + 
    'cd $OUT && ./source/runConfigureICU $platform --enable-static --enable-samples=no && make',
)

prebuilt_cxx_library(
  name = 'icudata',
  header_namespace = '',
  preferred_linkage = 'static',
  lib_name = 'icudata',
  lib_dir = '$(location :make)/lib',
  deps = [
    ':make',
  ],
)

prebuilt_cxx_library(
  name = 'icui18n',
  header_namespace = '',
  preferred_linkage = 'static',
  lib_name = 'icui18n',
  lib_dir = '$(location :make)/lib',
  deps = [
    ':make',
  ],
)

prebuilt_cxx_library(
  name = 'icuio',
  header_namespace = '',
  preferred_linkage = 'static',
  lib_name = 'icuio',
  lib_dir = '$(location :make)/lib',
  deps = [
    ':make',
  ],
)

prebuilt_cxx_library(
  name = 'icutu',
  header_namespace = '',
  preferred_linkage = 'static',
  lib_name = 'icutu',
  lib_dir = '$(location :make)/lib',
  deps = [
    ':make',
  ],
)

prebuilt_cxx_library(
  name = 'icuuc',
  header_namespace = '',
  preferred_linkage = 'static',
  lib_name = 'icuuc',
  lib_dir = '$(location :make)/lib',
  deps = [
    ':make',
  ],
)

prebuilt_cxx_library(
  name = 'icu4c',
  header_only = True,
  header_namespace = 'unicode',
  preferred_linkage = 'static',
  exported_headers = subdir_glob([
    ('source/common/unicode', '*.h'),
    ('source/i18n/unicode', '*.h'),
  ]),
  exported_preprocessor_flags = [
    '-DU_STATIC_IMPLEMENTATION',
  ],
  exported_deps = [
    ':icudata',
    ':icui18n',
    ':icuio',
    ':icutu',
    ':icuuc',
  ],
  visibility = [
    'PUBLIC',
  ],
)
