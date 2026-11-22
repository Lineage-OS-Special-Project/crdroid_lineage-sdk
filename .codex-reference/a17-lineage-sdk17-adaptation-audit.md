# Android 17 lineage-sdk adaptation audit

## Trust public-key notification adaptation

Updated the installed workflow script at `/home/yehudi/bin/losp-tools/adapt_lineage-sdk17.sh` to run the existing Trust public-key warning adaptation after the battery-default step. The Trust transform removes only the four-line `getKeysStatus()` / `TRUST_WARN_PUBLIC_KEY` notification block from `TrustInterfaceService.java`; it stops without modifying the source when the block differs unexpectedly. Re-running after application is recognized as already applied.

The Trust commit remains a separate signed-off commit with an explicit file path and separate subject and body `-m` arguments matching the patch. Its temporary-index commit now synchronizes the committed Trust path into the real index after HEAD advances, preserving unrelated staged entries. Apply, commit, and push prompts remain separate.

## Verification

- `bash -n` on the installed script: passed.
- Temporary Git fixture: first application removes only the public-key warning block and preserves SELinux checks: passed.
- Temporary Git fixture: repeated application is clean and idempotent: passed.
- Temporary Git fixture: unexpected source variant exits with an error and leaves the source unchanged: passed.
- Temporary Git fixture: declining commit leaves the adaptation in the worktree without creating a commit: passed.
- Temporary Git fixture: committing with an unrelated staged file creates a signed-off Trust-only commit, leaves the unrelated staged file staged, and leaves the committed Trust file synchronized with HEAD in the real index: passed.

All workflow verification performed for this update used disposable repositories under `/tmp`; this task did not run the installed workflow against the live repository or create or push a live commit.

## Report discovery

No existing lineage-sdk adaptation audit report was present in the repository, its parent checkout, or `/home/yehudi/bin/losp-tools`. This report was created at:

`/home/BUILDS/repos/LOSP-17.0/lineage-sdk/.codex-reference/a17-lineage-sdk17-adaptation-audit.md`
