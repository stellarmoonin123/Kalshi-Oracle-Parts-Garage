# Oracle — repaired original system (2026-09-29)

[Download the complete source ZIP](complete-source.zip)

This is the complete repaired original Kalshi Oracle system from PR #25, packaged as a separate garage entry. It is not the separate Oracle 2.1 rebuild.

## Contents
All 1,414 tracked files: API/trading engine, dashboard, shared packages, tests, configuration, dependency lockfile, operational scripts, checkpoints, and documentation. No installed dependencies or local environment files are included. The tracked paper ledger is a zero-trade seed.

## Provenance
- Source repository: stellarmoonin123/Kalshi-oracle
- Source branch: codex/master-production-readiness-20260929
- Source commit: 5c78c01a02a23e412c4d4fa4c877bfadccd6f197
- Source tree: e9aa4272db40e48f565c5dca4dc6716cf26054fd
- ZIP SHA-256: eb1d344297dc95208db7e02142dfe0458dd0efa2df1c5fbc9b737f088687aac3
- PR: https://github.com/stellarmoonin123/Kalshi-oracle/pull/25

The ZIP was made from a local checkout with the identical source tree; local Git commit metadata differs from the source GitHub commit.

## Setup
1. Download and extract complete-source.zip.
2. Open the extracted Kalshi-Oracle-Repaired directory in Cursor or your terminal.
3. Use Node 22 and pnpm 10.14.0, and provision a disposable PostgreSQL database for initial validation.
4. Follow README.md, docs/START_HERE.md, and docs/accounts/ACCOUNTS.md for environment configuration and administrator setup. Supply your own credentials; do not commit them.
5. Install dependencies with `pnpm install --frozen-lockfile`.
6. Apply the schema to the disposable database with `pnpm db:push`.
7. Run `pnpm run dev:api` and `pnpm run dev:dashboard` in separate terminals.
8. Complete docs/PAPER_PRODUCTION_RELEASE_CHECKLIST.md before production use.

## Verification
Full disposable-PostgreSQL CI passed on the preceding repair commit d01bf189662f7997e1404f0ccd60cb27aa974b10:
https://github.com/stellarmoonin123/Kalshi-oracle/actions/runs/36620624362

- API: 3,364 passed, 0 failed, 482 skipped.
- Dashboard: 368 passed.
- Locked install, shared/workspace typechecks, test-output completeness checks, schema drift, production build, and dependency vulnerability gate passed.
- The packaged follow-up changes only the API runner's 120-second test timeout and its documentation. Focused checks passed (13 tests); full CI for this follow-up was not verified at packaging time.
- ZIP integrity was checked successfully.

The detailed repair report is inside docs/reviews/MASTER_READINESS_REPAIRS_2026-09-29.md. Skipped tests are not verified coverage. These results do not establish profitability or live-trading readiness.

## Operating scope
Paper safeguards and committed trading thresholds are preserved. This is a stored source snapshot, not a deployment or merge. Do not overwrite production databases or ledgers when trying it.
