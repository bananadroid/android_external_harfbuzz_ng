if not find_program('gtkdoc-scan', required: get_option('docs')).found()
  message('Not building documentation as gtk-doc was not found')
  subdir_done()
endif

conf.set('HAVE_GTK_DOC', 1)

gnome = import('gnome')

docconf = configuration_data()
docconf.set('HB_VERSION', meson.project_version())

version_xml = configure_file(input: 'version.xml.in',
  output: 'version.xml',
  configuration: docconf)

content_files = [
  'usermanual-what-is-harfbuzz.xml',
  'usermanual-install-harfbuzz.xml',
  'usermanual-getting-started.xml',
  'usermanual-glyph-information.xml',
  'usermanual-shaping-concepts.xml',
  'usermanual-object-model.xml',
  'usermanual-buffers-language-script-and-direction.xml',
  'usermanual-fonts-and-faces.xml',
  'usermanual-opentype-features.xml',
  'usermanual-clusters.xml',
  'usermanual-utilities.xml',
  'usermanual-integration.xml',
  version_xml,
]

html_images = [
  'HarfBuzz.png',
  'HarfBuzz.svg',
]

ignore_headers = [
  'hb-features.h',
  'hb-gobject.h',
  'hb-gobject-enums.h',
  'hb-gobject-enums-tmp.h',
  'hb-gobject-structs.h',
]

gnome.gtkdoc('harfbuzz',
  main_sgml: 'harfbuzz-docs.xml',
  src_dir: [meson.current_source_dir() / '..' / 'src',
            meson.current_build_dir() / '..' / 'src',
           ],
  scan_args: ['--deprecated-guards=HB_DISABLE_DEPRECATED',
              '--ignore-decorators=HB_EXTERN|HB_DEPRECATED|HB_DEPRECATED_FOR()',
             ],
  mkdb_args: ['--source-suffixes=h,cc',
              '--xml-mode',
              '--output-format=xml',
             ],
  content_files: content_files,
  html_assets: html_images,
  ignore_headers: ignore_headers,
  dependencies: [libharfbuzz_dep],
  install: true,
  check: true,
)
