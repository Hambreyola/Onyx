project('loom', 'c', default_options: ['c_std=c11', 'warning_level=2'])

# We add _POSIX_C_SOURCE to tell the compiler to allow POSIX functions
add_project_arguments([
    '-DWLR_USE_UNSTABLE',
    '-D_POSIX_C_SOURCE=200809L'
], language: 'c')

wlroots        = dependency('wlroots-0.19')
wayland_server = dependency('wayland-server')
wayland_protos = dependency('wayland-protocols')
xkbcommon      = dependency('xkbcommon')

wl_scanner = find_program('wayland-scanner')
wayland_protos_dir = wayland_protos.get_variable('pkgdatadir')

xdg_shell_xml = wayland_protos_dir + '/stable/xdg-shell/xdg-shell.xml'

xdg_shell_h = custom_target(
  'xdg-shell-protocol.h',
  output: 'xdg-shell-protocol.h',
  input: xdg_shell_xml,
  command: [wl_scanner, 'server-header', '@INPUT@', '@OUTPUT@'],
)

xdg_shell_c = custom_target(
  'xdg-shell-protocol.c',
  output: 'xdg-shell-protocol.c',
  input: xdg_shell_xml,
  command: [wl_scanner, 'private-code', '@INPUT@', '@OUTPUT@'],
)

executable(
  'loom',
  sources: ['src/tinywl.c', xdg_shell_h, xdg_shell_c],
  dependencies: [wlroots, wayland_server, xkbcommon],
)