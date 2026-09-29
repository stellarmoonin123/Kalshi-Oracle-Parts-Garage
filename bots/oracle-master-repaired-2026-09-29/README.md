# Oracle — repaired original system (2026-09-29)

[Download complete source](complete-source.zip) · [Follow-up audit and repairs](FOLLOWUP_AUDIT.md)

Complete 1,419-file source snapshot: API/trading engine, dashboard, shared packages, tests, dependency lockfile, scripts, checkpoints and documentation. This is the repaired original system, separate from the Oracle 2.1 rebuild. Installed dependencies and operational credentials are excluded.

## Source identity
- Source commit: 0eed37035e3e732871b6d4eec8765b8b8ec5af44
- Source tree: e9d4418693f5b80f407b883f3a20a007347c1394
- Branch: codex/master-production-readiness-20260929
- PR: https://github.com/stellarmoonin123/Kalshi-oracle/pull/25
- ZIP SHA-256: dffe5acd353dd08935d0418fc3d55d35a48d7f4a88e5b01e108f5c4e69137707

The ZIP was generated from a local Git checkout with an identical source tree; local commit metadata differs.

## Installation
Extract the ZIP and open Kalshi-Oracle-Repaired in Cursor. Use Node 22 and pnpm 10.14.0. Copy .env.example to .env and supply a disposable PostgreSQL database plus your administrator bootstrap settings. Run pnpm install --frozen-lockfile and pnpm db:push. Run pnpm run dev:api and pnpm run dev:dashboard in separate terminals. Follow README.md and docs/accounts/ACCOUNTS.md. Keep credentials local.

## Latest repairs
Anonymous health output excludes private balances and operational details. Damaged/unreadable existing configuration stops startup instead of silently resetting. Login identifier counters retain fixed-size hashes, are bounded and fail closed at capacity. Setup instructions and environment examples match account authentication. The repair branch now triggers PostgreSQL CI on pushes. The explicit code checkpoint is refreshed so restoring source retains the config startup guard. Saved trading settings are unchanged.

## Verification
Latest local checks passed: 82 focused tests (29 new/config regressions, 44 ledger/recovery/quote/fatal safety tests, and 9 checkpoint tests), shared/workspace typechecks, production build and all 368 dashboard tests.
Full PostgreSQL CI for this exact commit:
https://github.com/stellarmoonin123/Kalshi-oracle/actions/runs/36639403534
Status at packaging: running. No passing result is claimed yet for this commit.

Earlier full repair CI passed on d01bf189662f7997e1404f0ccd60cb27aa974b10: 3,364 API passes, 0 failures, 482 skips; 368 dashboard passes; install/typecheck/schema/build/audit gates passed.

## Release limits
Paper safeguards and trading thresholds are preserved. Replay, sustained paper operation and backup/recovery drills remain required. Persistence error handling and empty-volume seed initialization need broader validation; see the audit. Skipped tests are not verified coverage. No merge, deployment, live enablement or profitability certification is included.
