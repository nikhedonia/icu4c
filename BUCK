
remote_file(
  name = 'icu4c-data',
  out = 'icu4c-data.zip',
  type = 'exploded_zip',
  url = 'https://github.com/nikhedonia/icu4c.S/archive/ca722d76845bf951fad0a82e4dd3a06805aa009c.zip',
  sha1 = 'eb0f27b44dabc9035444fef8b0ee343027abb7d3',
)


path = '$(location :icu4c-data)/icu4c.S-ca722d76845bf951fad0a82e4dd3a06805aa009c/icudt59l_dat.S'

genrule(
  name = 'icudt59l_dat',
  srcs = [':icu4c-data'],
  out = 'icudt59l_dat.S',
  cmd = 'cp '+path+' $OUT'
)


cxx_library(
  name = 'icu4c',
  visibility = [
    'PUBLIC',
  ],

  exported_headers = subdir_glob([
     ('source/io', '**/*.h'),
     ('source/data', '**/*.h'),
     ('source/extra', '**/*.h'),
     ('source/i18n', '**/*.h'),
     ('source/common', '**/*.h'),
     ('source/common/unicode', '**/*.h'),
  ]),

  headers = glob([
    ('source/**/*.h')
  ], excludes = glob(['source/samples/**/*.h'])),

  srcs = [':icudt59l_dat'] + glob([
    'source/data/**/*.cpp',
    'source/io/**/*.cpp',
    #'source/io/**/*.c',
    #'source/extra/**/*.cpp',
    #'source/extra/**/*.c',
    'source/i18n/**/*.cpp',
    #'source/i18n/**/*.c',
    'source/common/**/*.cpp',
    #'source/common/**/*.c',
  ], excludes = glob([
    'source/**/*test.cpp',
    'source/samples/**/.cpp',
  ])),

  compiler_flags = [
    '-std=c++11'
  ],

  preprocessor_flags = [
    '-DUNISTR_FROM_CHAR_EXPLICIT=explicit',
    '-DUNISTR_FROM_STRING_EXPLICIT=explicit',
    '-DU_ENABLE_DYLOAD=1',
    '-DHAVE_DLFCN_H=1',
    '-DHAVE_DLOPEN=1',
    '-DU_IO_IMPLEMENTATION',
    '-DU_I18N_IMPLEMENTATION',
    '-DU_COMMON_IMPLEMENTATION',
  ],

  exported_platform_linker_flags = [
    ('default', ['-ldl']),
    ('^linux.*', ['-ldl'])
  ]
)
