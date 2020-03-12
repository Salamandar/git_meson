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
git diff --quiet HEAD && git diff --quiet --cached

for s in @0@ @1@ @2@; do
    sed -i -e 's|PRItime|PRIuMAX|g' "${s}"
done
xgettext -ogit.pot+                  @3@ @4@ @0@
xgettext -ogit.pot+ --join-existing  @3@ @5@ @1@
xgettext -ogit.pot+ --join-existing  @3@ @6@ @2@

# Reverting the munged source, leaving only the updated file
# git reset --hard
mv git.pot+ git.pot

'''.format(
    ' '.join(sources_localized_c),
    ' '.join(sources_localized_sh),
    ' '.join(sources_localized_perl),

    ' '.join(xgettext_flags),
    ' '.join(xgettext_flags_c),
    ' '.join(xgettext_flags_sh),
    ' '.join(xgettext_flags_perl),
)


custom_target('git.pot',
    output: 'git.pot',
    command: [ 'bash', '-c', translations_command ],
)
