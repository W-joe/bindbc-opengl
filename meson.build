## Build file for meson

project('bindbc-opengl', 'd',
	meson_version: '>=0.46.0',
	license: 'Boost',
	version: '0.9.0',
	subproject_dir: 'subprojects',
	default_options: [
		'buildtype=release',
		],
	)

compiler_id		= meson.get_compiler('d').get_id()
project_name		= meson.project_name()
project_target		= project_name + '_' + compiler_id
project_description	= 'A dynamic binding to the OpenGL library.'
project_homepage	= 'https://github.com/BindBC/bindbc-opengl'


## versions
module_versions = []

opengl_version = get_option('opengl_version')
module_versions += opengl_version

opengl_extensions = get_option('opengl_extensions')
module_versions += opengl_extensions


## Dependencies
bindbc_loader_dep = dependency('bindbc-loader_' + compiler_id,
	required: false,
	version: '>=0.2.0')

if not bindbc_loader_dep.found()
	bindbc_loader = subproject('bindbc-loader')
	bindbc_loader_dep = bindbc_loader.get_variable('bindbc_loader_dep')
endif


## Import directories
import_dir = include_directories(
	'source/',
	)

## Source Files
source_files = [
	'source/bindbc/opengl/config.d',
	'source/bindbc/opengl/context.d',
	'source/bindbc/opengl/gl.d',
	'source/bindbc/opengl/package.d',

	'source/bindbc/opengl/bind/gl11.d',
	'source/bindbc/opengl/bind/gl12.d',
	'source/bindbc/opengl/bind/gl13.d',
	'source/bindbc/opengl/bind/gl14.d',
	'source/bindbc/opengl/bind/gl15.d',
	'source/bindbc/opengl/bind/gl20.d',
	'source/bindbc/opengl/bind/gl21.d',
	'source/bindbc/opengl/bind/gl30.d',
	'source/bindbc/opengl/bind/gl31.d',
	'source/bindbc/opengl/bind/gl32.d',
	'source/bindbc/opengl/bind/gl33.d',
	'source/bindbc/opengl/bind/gl40.d',
	'source/bindbc/opengl/bind/gl41.d',
	'source/bindbc/opengl/bind/gl42.d',
	'source/bindbc/opengl/bind/gl43.d',
	'source/bindbc/opengl/bind/gl44.d',
	'source/bindbc/opengl/bind/gl45.d',
	'source/bindbc/opengl/bind/gl46.d',
	'source/bindbc/opengl/bind/package.d',
	'source/bindbc/opengl/bind/types.d',

	'source/bindbc/opengl/bind/arb/arb_01.d',
	'source/bindbc/opengl/bind/arb/core_30.d',
	'source/bindbc/opengl/bind/arb/core_31.d',
	'source/bindbc/opengl/bind/arb/core_32.d',
	'source/bindbc/opengl/bind/arb/core_33.d',
	'source/bindbc/opengl/bind/arb/core_40.d',
	'source/bindbc/opengl/bind/arb/core_41.d',
	'source/bindbc/opengl/bind/arb/core_42.d',
	'source/bindbc/opengl/bind/arb/core_43.d',
	'source/bindbc/opengl/bind/arb/core_44.d',
	'source/bindbc/opengl/bind/arb/core_45.d',
	'source/bindbc/opengl/bind/arb/core_46.d',
	'source/bindbc/opengl/bind/arb/package.d',
	]


## Target
target_lib = library(
	project_target,
	sources: source_files,
	include_directories: import_dir,
	dependencies: [bindbc_loader_dep],
	install: true,
	d_module_versions: module_versions,
	pic: true,
	)

install_subdir('source/bindbc/', install_dir: 'include/d/')


## Dependency
bindbc_opengl_dep = declare_dependency(
	include_directories: import_dir,
	link_with: target_lib,
	version: meson.project_version(),
	dependencies: bindbc_loader_dep,
	)


## pkg-config
pkgConf = import('pkgconfig')
pkgConf.generate(
	name: project_target,
	subdirs: 'd/',
	version: meson.project_version(),
	description: project_description,
	d_module_versions: module_versions,
	libraries: target_lib,
	)

