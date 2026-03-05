project('loom', 'c', default_options: ['c_std=c11', 'warning_level=2'])

# Add project arguments
add_project_arguments([
    '-DWLR_USE_UNSTABLE',
    '-D_POSIX_C_SOURCE=200809L'
], language: 'c')

# Dependencies
wlroots        = dependency('wlroots-0.19')
wayland_server = dependency('wayland-server')
wayland_protos = dependency('wayland-protocols')
xkbcommon      = dependency('xkbcommon')

# Tools
wl_scanner = find_program('wayland-scanner')
wayland_protos_dir = wayland_protos.get_variable('pkgdatadir')

# --- Protocol Generation: XDG Shell (Windows) ---
xdg_shell_xml = wayland_protos_dir + '/stable/xdg-shell/xdg-shell.xml'
xdg_shell_h = custom_target('xdg-shell-protocol.h', output: 'xdg-shell-protocol.h', input: xdg_shell_xml, command: [wl_scanner, 'server-header', '@INPUT@', '@OUTPUT@'])
xdg_shell_c = custom_target('xdg-shell-protocol.c', output: 'xdg-shell-protocol.c', input: xdg_shell_xml, command: [wl_scanner, 'private-code', '@INPUT@', '@OUTPUT@'])

# --- Protocol Generation: Layer Shell ---
layer_shell_xml = files('protocols/wlr-layer-shell-unstable-v1.xml')

layer_shell_h = custom_target(
    'wlr-layer-shell-unstable-v1-protocol.h',
    output: 'wlr-layer-shell-unstable-v1-protocol.h',
    input: layer_shell_xml,
    command: [wl_scanner, 'server-header', '@INPUT@', '@OUTPUT@']
)

layer_shell_c = custom_target(
    'wlr-layer-shell-unstable-v1-protocol.c',
    output: 'wlr-layer-shell-unstable-v1-protocol.c',
    input: layer_shell_xml,
    command: [wl_scanner, 'private-code', '@INPUT@', '@OUTPUT@']
)

# The Executable
executable(
  'loom',
  sources: [
    'src/tinywl.c', 
    xdg_shell_h, xdg_shell_c, 
    layer_shell_h, layer_shell_c
  ],
  dependencies: [wlroots, wayland_server, xkbcommon],
)