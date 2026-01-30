project(
    'phnt',
    'c',
    meson_version: '>=0.63.0',
    # last two components are calculated as:
    # ```bash
    # export TZ=UTC
    # timestamp="$(git -C systeminformer show ${commit} -q --format=%at)"
    # minor="$(date +%y%j --date=@${timestamp})"
    # patch="$(date +%-H0%0M --date=@${timestamp})"
    # patch="$((${patch} + 1000))"
    # echo "${minor}.${patch}"
    # ```
    version: '3.4.26021.21047',
)

cc = meson.get_compiler('c')
ntdll_dep = cc.find_library('ntdll')

phnt_inc = include_directories('.')

phnt_srcs = files(
    'ntafd.h',
    'ntbcd.h',
    'ntdbg.h',
    'ntexapi.h',
    'ntgdi.h',
    'ntimage.h',
    'ntintsafe.h',
    'ntioapi.h',
    'ntkeapi.h',
    'ntldr.h',
    'ntlpcapi.h',
    'ntmisc.h',
    'ntmmapi.h',
    'ntnls.h',
    'ntobapi.h',
    'ntpebteb.h',
    'ntpfapi.h',
    'ntpnpapi.h',
    'ntpoapi.h',
    'ntpsapi.h',
    'ntregapi.h',
    'ntrtl.h',
    'ntsam.h',
    'ntseapi.h',
    'ntsmss.h',
    'ntstrsafe.h',
    'ntsxs.h',
    'nttmapi.h',
    'nttp.h',
    'ntuser.h',
    'ntwmi.h',
    'ntwow64.h',
    'ntxcapi.h',
    'ntzwapi.h',
    'phnt.h',
    'phnt_ntdef.h',
    'phnt_windows.h',
    'smbios.h',
    'subprocesstag.h',
    'usermgr.h',
    'winsta.h',
)

install_headers(
    phnt_srcs,
    subdir: 'phnt',
)

phnt_dep = declare_dependency(
    include_directories: phnt_inc,
    dependencies: ntdll_dep,
)

meson.override_dependency('phnt', phnt_dep)

pkgconfig = import(
    'pkgconfig',
    required: false,
)
if pkgconfig.found()
    pkgconfig.generate(
        name: 'phnt',
        description: 'Native API header files for the System Informer project.',
        url: 'https://github.com/winsiderss/phnt',
        libraries: ntdll_dep,
        install_dir: get_option('datadir') / 'pkgconfig',
        subdirs: 'phnt',
    )
endif
