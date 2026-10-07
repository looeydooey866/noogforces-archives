# NoogForces public archives

This repository stores public practice bugaboo packages and statement bundles
for [NoogForces](https://noogforces.vercel.app). It does not contain application
source, database credentials, accounts, submissions, or environment files.

The collection contains 717 USACO bugaboos (2011–2026) and 184 Singapore
NOI bugaboos (1999–2026), including four C++ linked-grader tasks: Ask One Get One
Free (2015), City Mapping (2018), Square or Rectangle (2019 preliminary), and
Shuffle (2019). Other multi-process jury tasks and tasks without usable published
data remain excluded. Original source attribution and licensing
information are retained in each package's `bugaboo.json` and statements; this
repository does not grant new rights to the original content.

## Release files

- `ID-SHA256.zip`: the complete NoogForces bugaboo package for importing/judging.
- `ID-SHA256.statements.zip`: lightweight statements and image/font assets for
  the website reader; not a standalone judging package.

Releases are split at 400 bugaboos (800 assets) to stay below GitHub's 1,000-asset
limit. Every asset is below 2 GiB. Filenames contain the complete-package SHA-256
checksum and are immutable. The publisher checks upload size/state and GitHub's
SHA-256 digest when available before making a marketplace record public.

## Verification limitations

The 897 standard packages passed structural checks, and the four additional
linked-grader packages passed package validation. Official reference solutions
achieved full scores for 585 USACO and 45 NOI packages. The remaining packages
have partial, failed, or unavailable reference checks; publication is not a claim
that every official reference program is correct. Inferred 2024 NOI subtask
memberships warrant independent review. Participant-contributed solutions were
removed from distributed packages.

City Mapping and Square or Rectangle also achieved full scores in local reference
checks. Shuffle was checked with an independent API-only oracle on its samples,
including rejection of wrong results and invalid queries; this is not a full
solution verification. Ask One Get One Free has not had a full reference check.
The judge supports linked C++ graders and single-process stdin/stdout interactors,
not every multi-process contest manager protocol.

## Publishing from the application workspace

Sign in with `gh auth login`. The target repository must already be public; the
publisher never changes a repository's visibility. Database credentials stay in
the ignored `apps/web/.env.local`, and GitHub authentication stays in the CLI.

```sh
node --import tsx scripts/publish-archive.ts dist/usaco usaco "USA Computing Olympiad" --github-repo=looeydooey866/noogforces-archives --workers=4
node --import tsx scripts/publish-archive.ts dist/noisg noisg "Singapore National Olympiad in Informatics" --github-repo=looeydooey866/noogforces-archives
node --import tsx scripts/publish-archive.ts dist/noisg-graders noisg "Singapore National Olympiad in Informatics" --github-repo=looeydooey866/noogforces-archives --release=noisg-graders-2026-10-07
```

Reruns skip matching published packages and resume matching release assets without
overwriting them. Confirmed unpublished `starter` upload placeholders are removed
and retried; completed assets are never replaced. Large ZIPs are processed
individually to limit memory use.
Packages are listed only after both the judging ZIP and reading bundle are stored.
Downloads redirect from NoogForces to GitHub, avoiding Vercel's file-transfer limits.
The website fetches only small statement bundles and sanitizes HTML/Markdown.

Native submissions and checkers execute with the local user's permissions. Only
install and run packages you trust.
