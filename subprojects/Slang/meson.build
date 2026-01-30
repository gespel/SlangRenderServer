project(
  'slang',
  'c',
  version: '1.0.1',
  default_options: [
    'c_std=c11',
    'warning_level=3',
  ]
)

# Debug Option
slang_debug = get_option('slang_debug')
if slang_debug
  add_project_arguments('-DSLANG_DEBUG', language: 'c')
endif

# ============================================================================
# Core Sources and Headers
# ============================================================================
core_sources = [
  'core/src/buffer_core.c',
  'core/src/function.c',
  'core/src/interpreter.c',
  'core/src/parser.c',
  'core/src/rack.c',
  'core/src/tokenizer.c',
  'core/src/tools.c',
]

core_headers = [
  'core/include/buffer_core.h',
  'core/include/core_types.h',
  'core/include/function.h',
  'core/include/interpreter.h',
  'core/include/parser.h',
  'core/include/rack.h',
  'core/include/tokenizer.h',
  'core/include/tools.h',
  'core/include/variable.h',
]

# ============================================================================
# Oscillators Module
# ============================================================================
osc_sources = [
  'modules/oscillators/src/oscillator.c',
  'modules/oscillators/src/sine.c',
  'modules/oscillators/src/square.c',
  'modules/oscillators/src/sawtooth.c',
  'modules/oscillators/src/triangle.c',
  'modules/oscillators/src/terrain.c',
  'modules/oscillators/src/wavetable.c',
]

osc_headers = [
  'modules/oscillators/include/oscillator.h',
  'modules/oscillators/include/oscillator_types.h',
  'modules/oscillators/include/sine.h',
  'modules/oscillators/include/square.h',
  'modules/oscillators/include/sawtooth.h',
  'modules/oscillators/include/triangle.h',
  'modules/oscillators/include/terrain.h',
  'modules/oscillators/include/wavetable.h',
]

# ============================================================================
# Envelope Module
# ============================================================================
envelope_sources = [
  'modules/envelope/src/envelope.c',
  'modules/envelope/src/linenvelope.c',
]

envelope_headers = [
  'modules/envelope/include/envelope.h',
  'modules/envelope/include/envelope_types.h',
  'modules/envelope/include/linenvelope.h',
]

# ============================================================================
# Filters Module
# ============================================================================
filter_sources = [
  'modules/filters/src/lowpassfilter.c',
]

filter_headers = [
  'modules/filters/include/filter_types.h',
  'modules/filters/include/lowpassfilter.h',
]

# ============================================================================
# Step Sequencer Module
# ============================================================================
step_sources = [
  'modules/stepsequencer/src/stepsequencer.c',
]

step_headers = [
  'modules/stepsequencer/include/stepsequencer.h',
  'modules/stepsequencer/include/stepsequencer_types.h',
]

# ============================================================================
# Sample Source Module
# ============================================================================
sample_source_sources = [
  'modules/sample-source/src/sample_source.c',
]

sample_source_headers = [
  'modules/sample-source/include/sample_source.h',
]

# ============================================================================
# Data Module
# ============================================================================
data_sources = [
  'modules/data/src/binaryData.c',
]

data_headers = [
  'modules/data/include/binaryData.h',
]

# ============================================================================
# Create Slang Library
# ============================================================================
slang_lib = shared_library(
  'slang',
  core_sources +
  core_headers +
  osc_sources +
  osc_headers +
  envelope_sources +
  envelope_headers +
  filter_sources +
  filter_headers +
  step_sources +
  step_headers +
  sample_source_sources +
  sample_source_headers +
  data_sources +
  data_headers,
  include_directories: include_directories(
    'core/include',
    'modules/oscillators/include',
    'modules/envelope/include',
    'modules/filters/include',
    'modules/stepsequencer/include',
    'modules/sample-source/include',
    'modules/data/include',
  ),
  dependencies: [],
  link_args: ['-lm'],
  install: true
)

# ============================================================================
# Create Header Library (for consumers)
# ============================================================================
slang_headers = custom_target(
  'slang_headers',
  command: ['echo', 'Slang headers installed'],
  output: 'headers_dummy',
  install: true,
  install_dir: get_option('includedir') / 'slang'
)

# ============================================================================
# Test Executables
# ============================================================================
tester_exe = executable(
  'tester',
  'tester.c',
  include_directories: include_directories(
    'core/include',
    'modules/oscillators/include',
    'modules/envelope/include',
    'modules/filters/include',
    'modules/stepsequencer/include',
    'modules/sample-source/include',
    'modules/data/include',
  ),
  link_with: slang_lib,
  link_args: ['-lm'],
  install: true
)

slang_exe = executable(
  'slang',
  'slang.c',
  include_directories: include_directories(
    'core/include',
    'modules/oscillators/include',
    'modules/envelope/include',
    'modules/filters/include',
    'modules/stepsequencer/include',
    'modules/sample-source/include',
    'modules/data/include',
  ),
  link_with: slang_lib,
  link_args: ['-lm'],
  install: true
)

# ============================================================================
# Summary
# ============================================================================
summary({
  'Project': 'Slang',
  'Version': meson.project_version(),
  'Debug': slang_debug,
  'Oscillators': 'sine, square, sawtooth, triangle, terrain, wavetable',
  'Filters': 'lowpass',
  'Envelopes': 'ADSR, Linear',
  'Other Modules': 'step sequencer, sample source, binary data',
}, section: 'Slang Configuration')
# ============================================================================
# Export for parent project
# ============================================================================
set_variable('slang_lib', slang_lib)
