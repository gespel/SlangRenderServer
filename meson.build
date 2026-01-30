project(
  'SlangRenderServer',
  'c',
  version: '1.0.0',
  default_options: [
    'c_std=c11',
    'buildtype=release',
    'warning_level=3',
  ]
)

# Subprojekt Slang
slang_subproject = subproject('Slang')
slang_lib = slang_subproject.get_variable('slang_lib')

# RenderServer Sources
server_sources = [
  'server.c',
]

server_headers = [
  'server.h',
]

# RenderServer executable
render_server = executable(
  'SlangRenderServer',
  server_sources,
  include_directories: include_directories('subprojects/Slang/core/include', 'subprojects/Slang/modules'),
  link_with: slang_lib,
  link_args: ['-lm'],
  install: true
)

# Summary
summary({
  'Project': 'SlangRenderServer',
  'Version': meson.project_version(),
  'Build type': get_option('buildtype'),
  'Slang Library': 'included as subproject',
}, section: 'Configuration')
