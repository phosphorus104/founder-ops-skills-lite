---
name: release-notes
description: >-
  Turns the commits since the last release tag into three things: a CHANGELOG.md entry, customer-facing release notes in the product's voice, and a 280-character summary for a post. Groups changes by what the customer notices (new, improved, fixed), drops internal noise, and flags anything that needs a migration note. Use before tagging a release, or when asked "what changed since vX".
argument-hint: "[since-tag-or-ref] [new-version]"
allowed-tools: Bash(git log:*) Bash(git describe:*) Bash(git diff:*) Bash(git show:*) Bash(git rev-list:*) Bash(git tag:*) Bash(date:*) Read Grep
---

# Release notes

Three audiences read a release differently: a developer wants the changelog, a customer wants to know what got better, a follower wants one line. Write all three from the same facts.

## Inputs

- `$0`: the ref to start from. If empty, use `git describe --tags --abbrev=0` (the latest tag). If there is no tag, use the first commit (`git rev-list --max-parents=0 HEAD`) and say so.
- `$1`: the version being released. If empty, propose one by semver from the changes (breaking → major, feature → minor, fixes only → patch) and mark it "proposed".
- From `CLAUDE.md`: changelog path, where release notes are posted, voice, words customers use, commit convention.

Gather: `git log <since>..HEAD --no-merges --format='%h %s%n%b'` and, for anything unclear, `git diff <since>..HEAD --stat` and the diff of the specific file. Read the code change before describing it; a commit message is a hint, not a fact.

## Method

1. Drop internal noise: dependency bumps with no customer effect, CI, lint, formatting, test-only changes, typo fixes in code comments. Keep them in a one-line "Internal" tally in the changelog only.
2. Translate each remaining change into what the customer notices. "Refactor invoice service" becomes nothing; "invoice PDFs now show the tax ID" becomes a line.
3. Group: **New**, **Improved**, **Fixed** (in the changelog these are Keep a Changelog's **Added**, **Changed**, **Fixed**; removed features go under **Removed** in the changelog and under **Action needed** in the notes). Within a group, order by how many customers it touches.
4. Spot migrations: schema changes, renamed settings, changed defaults, removed features, new permissions. Each gets an **Action needed** line with the exact step.
5. Use the customer's words from `CLAUDE.md`. Never use the internal name of a module in customer-facing text.
6. One sentence per change, under 20 words, starting with a noun or verb, no "we're excited".

## Output

Print, in this order:

### 1. CHANGELOG entry (Keep a Changelog style, paste at the top of the changelog file)

```
## [<version>] - <YYYY-MM-DD>
### Added
- ...
### Changed
- ...
### Fixed
- ...
### Internal
- <n> dependency updates, <n> test and CI changes
```

### 2. Release notes (customer-facing)

```
# <Product> <version>: <the one thing this release is about>

<One sentence on who benefits and how.>

**New**
- ...
**Improved**
- ...
**Fixed**
- ...
**Action needed** (omit the section if none)
- ...

Questions or something off? Reply to this email.
```

### 3. Summary post (≤ 280 characters; no hashtags or emoji unless `CLAUDE.md` asks for them)

Then: "Commits read: <n>. Dropped as internal: <n>. Unclear and needs your word: <list, or none>." Do not write to files or create the tag unless asked.

## Checklist

- [ ] Every customer-facing line maps to at least one commit or diff hunk you read.
- [ ] No line describes code structure; every line describes an effect a user can see or a step they must take.
- [ ] Breaking changes appear in all three outputs, with the step to take.
- [ ] Version follows semver from the content, not from habit.
- [ ] Voice matches `CLAUDE.md`; banned words absent.

## Pitfalls

- Squash-merged PRs hide several changes in one commit; read the PR body in the commit body.
- A reverted commit and its revert cancel out; show neither and count neither.
- Security fixes: describe the fix and the affected versions, never the exploit.
