xgettext_flags = [
    '--force-po',
    '--add-comments=TRANSLATORS:',
    '--msgid-bugs-address="Git Mailing List <git@vger.kernel.org>"',
    '--from-code=UTF-8',
]
xgettext_flags_c = [
    '--language=C',
    '--keyword=_',
    '--keyword=N_',
    '--keyword=Q_:1,2',
]
xgettext_flags_sh = [
    '--keyword=gettextln',
    '--keyword=eval_gettextln',
]
xgettext_flags_perl = [
    '--keyword=__',
    '--keyword=N__',
    '--keyword=__n:1,2'
]

translations_command = '''
# All modifications will be reverted at the end, so we do not
# want to have any local change.
if ! git diff --quiet HEAD && git diff --quiet --cached; then
    echo; echo "Error: Some changes are uncommited!"; echo
    exit 1
fi

for s in @0@ @1@ @2@; do
    sed -i -e 's|PRItime|PRIuMAX|g' "${s}"
done

out="po/git.pot"
rm -f "${out}"
xgettext -o"${out}"                  @3@ @4@ @0@ 2>/dev/null
xgettext -o"${out}" --join-existing  @3@ @5@ @1@ 2>/dev/null
xgettext -o"${out}" --join-existing  @3@ @6@ @2@ 2>/dev/null

# Reverting the munged source, leaving only the updated file
# git reset --hard

'''.format(
    ' '.join(localized_c),
    ' '.join(localized_sh),
    ' '.join(localized_perl),

    ' '.join(xgettext_flags),
    ' '.join(xgettext_flags_c),
    ' '.join(xgettext_flags_sh),
    ' '.join(xgettext_flags_perl),
)


custom_target('git.pot',
    output: 'git.pot',
    command: [ 'bash', '-e', '-c', translations_command ],
)
