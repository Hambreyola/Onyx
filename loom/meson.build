project(
  'loom',
  'c',
  version: '0.1.0',
  default_options: [
    'c_std=c11',
    'warning_level=2',
    'werror=true',
  ],
)

# Grab the dependencies we need from the system
wlroots = dependency('wlroots') 
wayland_server = dependency('wayland-server')
xkbcommon = dependency('xkbcommon')

# Define the executable
executable(
  'loom',
  sources: ['src/tinywl.c'],
  dependencies: [
    wlroots,
    wayland_server,
    xkbcommon,
  ],
  install: true,
)