project('epiphany', 'c',
  license: 'GPL3+',
  version: '3.25.3',
  meson_version: '>= 0.37.0',
  default_options: ['c_std=gnu11']
)

gnome = import('gnome')
i18n = import('i18n')

prefix = get_option('prefix')
datadir = join_paths(prefix, get_option('datadir'))
libdir = join_paths(prefix, get_option('libdir'))
libexecdir = join_paths(prefix, get_option('libexecdir'))
localedir = join_paths(prefix, get_option('localedir'))
pkgdatadir = join_paths(datadir, 'epiphany')
pkglibdir = join_paths(libdir, 'epiphany')
pkglibexecdir = join_paths(libexecdir, 'epiphany')
webextensionsdir = join_paths(pkglibdir, 'web-extensions')

iso_codes = dependency('iso-codes')
iso_codes_prefix = iso_codes.get_pkgconfig_variable('prefix')

conf = configuration_data()
conf.set_quoted('BUILD_ROOT', meson.build_root())
conf.set_quoted('DISTRIBUTOR_NAME', get_option('distributor_name'))
conf.set_quoted('EPHY_WEB_EXTENSIONS_DIR', webextensionsdir)
conf.set_quoted('GETTEXT_PACKAGE', meson.project_name())
conf.set_quoted('ISO_CODES_PREFIX', iso_codes_prefix)
conf.set_quoted('LOCALEDIR', localedir)
conf.set_quoted('PKGDATADIR', pkgdatadir)
conf.set_quoted('PKGLIBEXECDIR', pkglibexecdir)
conf.set_quoted('SOURCE_ROOT', meson.source_root())
conf.set_quoted('VERSION', meson.project_version())

conf.set10('ENABLE_NLS', true)
conf.set10('ENABLE_FIREFOX_SYNC', get_option('enable_firefox_sync'))
conf.set10('ENABLE_HTTPS_EVERYWHERE', get_option('enable_https_everywhere'))

configure_file(
  output: 'config.h',
  configuration: conf
)

glib_requirement = '>= 2.46.0'
gtk_requirement = '>= 3.22.13'
webkitgtk_requirement = '>= 2.17.3'

cairo_dep = dependency('cairo', version: '>= 1.2')
gcr_dep = dependency('gcr-3', version: '>= 3.5.5')
gdk_dep = dependency('gdk-3.0', version: gtk_requirement)
gdk_pixbuf_dep = dependency('gdk-pixbuf-2.0', version: '>= 2.36.5')
gio_dep = dependency('gio-2.0', version: glib_requirement)
gio_unix_dep = dependency('gio-unix-2.0', version: glib_requirement)
glib_dep = dependency('glib-2.0', version: glib_requirement)
gnome_desktop_dep = dependency('gnome-desktop-3.0', version: '>= 2.91.2')
gtk_dep = dependency('gtk+-3.0', version: gtk_requirement)
gtk_unix_print_dep = dependency('gtk+-unix-print-3.0', version: gtk_requirement)
icu_uc_dep = dependency('icu-uc', version: '>= 4.6')
iso_codes_dep = dependency('iso-codes', version: '>= 0.35')
json_glib_dep = dependency('json-glib-1.0', version: '>= 1.2.0')
libnotify_dep = dependency('libnotify', version: '>= 0.5.1')
libsecret_dep = dependency('libsecret-1', version: '>= 0.14')
libsoup_dep = dependency('libsoup-2.4', version: '>= 2.48.0')
libxml_dep = dependency('libxml-2.0', version: '>= 2.6.12')
libxslt_dep = dependency('libxslt', version: '>= 1.1.7')
sqlite3_dep = dependency('sqlite3', version: '>= 3.0')
webkit2gtk_dep = dependency('webkit2gtk-4.0', version: webkitgtk_requirement)
webkit2gtk_web_extension_dep = dependency('webkit2gtk-web-extension-4.0', version: webkitgtk_requirement)

cc = meson.get_compiler('c')
m_dep = cc.find_library('m', required: false)

if get_option('enable_firefox_sync')
  nettle_requirement = '>= 3.2'
  hogweed_dep = dependency('hogweed', version: nettle_requirement)
  nettle_dep = dependency('nettle', version: nettle_requirement)
  gmp_dep = cc.find_library('gmp')
endif

if get_option('enable_https_everywhere')
  httpseverywhere_dep = dependency('httpseverywhere-0.4', version: '>= 0.2.2')
endif

subdir('data')
subdir('help')
subdir('po')
subdir('lib')
subdir('embed')
subdir('src')
subdir('tests')

meson.add_install_script('post_install.py')
