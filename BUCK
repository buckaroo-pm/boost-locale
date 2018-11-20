load('//:buckaroo_macros.bzl', 'buckaroo_deps')

posix_srcs = glob([
  'src/posix/**/*.cpp', 
])

icu_srcs = glob([
  'src/icu/**/*.cpp', 
])

windows_srcs = glob([
  'src/win32/**/*.cpp', 
])

platform_srcs = posix_srcs + icu_srcs + windows_srcs

macos_preprocessor_flags = [
  '-DBOOST_LOCALE_WITH_ICU=1', 
  '-DBOOST_LOCALE_NO_WINAPI_BACKEND=1', 
]

linux_preprocessor_flags = [
  '-DBOOST_LOCALE_WITH_ICU=1', 
  '-DBOOST_LOCALE_NO_WINAPI_BACKEND=1', 
]

cxx_library(
  name = 'locale', 
  header_namespace = 'boost', 
  exported_headers = subdir_glob([
    ('include/boost', '**/*.hpp'), 
  ]), 
  platform_preprocessor_flags = [
    ('macos.*', macos_preprocessor_flags), 
    ('linux.*', linux_preprocessor_flags), 
  ], 
  srcs = glob([
    'src/**/*.cpp', 
  ], exclude = platform_srcs), 
  platform_srcs = [
    ('linux.*', posix_srcs + icu_srcs), 
    ('macos.*', posix_srcs + icu_srcs), 
    ('windows.*', windows_srcs), 
  ], 
  deps = buckaroo_deps(), 
  visibility = [
    'PUBLIC', 
  ], 
)
