sources = run_command('find', '.', '-name', '*.cpp').stdout().strip().split('\n')

wlr_protocol_dir = '../wlr-proto/'
cloth_protocol_dir = '../protocol/'

protocols = [
	[wp_protocol_dir, 'unstable/xdg-shell/xdg-shell-unstable-v6.xml'],
	[wp_protocol_dir, 'stable/xdg-shell/xdg-shell.xml'],
	[wp_protocol_dir, 'unstable/idle-inhibit/idle-inhibit-unstable-v1.xml'],
	[wlr_protocol_dir, 'idle.xml'],
	[wlr_protocol_dir, 'wlr-export-dmabuf-unstable-v1.xml'],
	[wlr_protocol_dir, 'wlr-input-inhibitor-unstable-v1.xml'],
	[wlr_protocol_dir, 'wlr-layer-shell-unstable-v1.xml'],
]

xml_files = []

foreach p : protocols
	xml = join_paths(p)
	xml_files += xml
endforeach

protocol_sources = custom_target('lock-protocols',
    input: xml_files,
    output: ['protocols.hpp', 'protocols.cpp'],
    command: [find_program('wayland-scanner++'), '@INPUT@', '@OUTPUT0@', '@OUTPUT1@'])

sources += protocol_sources

pam_dep =meson.get_compiler('cpp').find_library('pam')

executable(
	'cloth-lock',
	sources,
	dependencies: [
		thread_dep,
		fmt,
		wlroots,
		libinput,
		wayland_cursor_dep,
		dep_cloth_common,
		waylandpp,
		gtkmm,
		pam_dep
	],
	install: true
)
