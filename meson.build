project('git',
    'c',


)


vcs_tag(
    input : 'GIT-VERSION-FILE.in',
    output: 'GIT-VERSION-FILE',
    command: [ 'GIT-VERSION-GEN' ],
    replace_string: '@GIT_VERSION_TEXT@',
)


###############################################################################
# Tools

diff = find_program('diff')
tar  = find_program('tar')
find = find_program('find')
tcl  = find_program('ctlsh', required: false)
tcltk= find_program('wish')
curlconf= find_program('curl-config')
spatch  = find_program('spatch', required: false)

###############################################################################
# Dependencies

threads = dependency('threads')


###############################################################################
# Directories

gitexecdir = get_option('prefix') / 'libexec' / 'git-core'
mergetoolsdir = gitexecdir / 'mergetools'

gitwebdir   = get_option('datadir') / 'gitweb'
perllibdir  = get_option('datadir') / 'perl5'
templatedir = get_option('datadir') / 'git-core' / 'templates'
htmldir     = get_option('datadir') / 'doc' / 'git-doc'

gitconfig   = get_option('sysconfdir') / 'gitconfig'
gitattributes=get_option('sysconfdir') / 'gitattributes'



###############################################################################
###############################################################################
# Sources

localized_sh = []
localized_c  = []


###############################################################################
# Install scripts
scripts_sh = [
    'git-bisect',
    'git-difftool--helper',
    'git-filter-branch',
    'git-legacy-stash',
    'git-merge-octopus',
    'git-merge-one-file',
    'git-merge-resolve',
    'git-mergetool',
    'git-quiltimport',
    'git-request-pull',
    'git-submodule',
    'git-web--browse',
]

scripts_lib = [
    'git-mergetool--lib',
    'git-parse-remote',
    'git-rebase--preserve-merges',
    'git-sh-setup',
    'git-sh-i18n',
]

scripts_perl = [
    'git-add--interactive',
    'git-archimport',
    'git-cvsexportcommit',
    'git-cvsimport',
    'git-cvsserver',
    'git-send-email',
    'git-svn',
]

scripts_python = [
    'git-p4',
]

localized_sh += scripts_sh + scripts_lib



subdir('po')
