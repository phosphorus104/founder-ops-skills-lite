<!-- Worked example for a fictional product, "Ledgerly". Its CLAUDE.md names the product, posts release notes at ledgerly.app/changelog, and lists "customer" as the word customers use. No version was given, so the skill proposed one. -->

Proposed version 1.5.0 (minor): two features, one renamed setting with a redirect, no breaking change.

### 1. CHANGELOG entry

## [1.5.0] - 2026-10-05
### Added
- Invoice PDFs show the customer's tax ID when it is set on the customer record.
### Changed
- Pro plan API rate limit raised from 60 to 120 requests per minute; `X-RateLimit-Limit` now reports the plan's limit.
- "Export" is renamed "Download data" and moved under Settings → Data; the old /export route redirects for 90 days.
### Fixed
- Weekly report emails sent at 00:00 local time now cover the local day instead of the UTC day (#212).
- Tables pasted into the editor keep their column widths.
### Internal
- 1 dependency update, 1 test change, 1 refactor with no behaviour change.

### 2. Release notes

# Ledgerly 1.5.0: tax IDs on invoice PDFs

If you bill clients who need a tax ID, it now appears on the invoice PDF once it is set on the customer record.

**New**
- Invoice PDFs include the customer's tax ID when you have filled it in on the customer record.

**Improved**
- Pro plans can now make 120 API requests a minute, up from 60.

**Fixed**
- Weekly report emails sent at midnight now cover your local day.
- Tables pasted into the editor keep their column widths.

**Action needed**
- "Export" is now "Download data" under Settings → Data. Update bookmarks that point to /export; the old link redirects for 90 days.

Questions or something off? Reply to this email.

### 3. Summary post

Ledgerly 1.5.0: customer tax IDs on invoice PDFs, Pro API limit up to 120 req/min, midnight report emails fixed. "Export" is now Settings → Data → Download data. Notes: ledgerly.app/changelog

Commits read: 8. Dropped as internal: 3 (dependency bump, test, refactor). Unclear and needs your word: none.
