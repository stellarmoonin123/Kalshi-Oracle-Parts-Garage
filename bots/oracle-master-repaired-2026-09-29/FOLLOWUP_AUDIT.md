# Follow-up source audit — 2026-09-29

Scope: repaired original Oracle system, based on source commit 5c78c01a02a23e412c4d4fa4c877bfadccd6f197. This does not audit the separate Oracle 2.1 rebuild or certify live trading.

## Confirmed defects repaired

| Severity | Evidence | Failure | Repair and acceptance |
| --- | --- | --- | --- |
| High | routes/health.ts returns knownCents, error details, build identity and subsystem state on public /healthz | Anonymous callers could read private desk information | Anonymous response uses an explicit two-field allowlist; authenticated report remains compatible. Regression verifies private fields are absent. |
| High | lib/config-persist.ts catches every load error and returns an empty object | Existing damaged or unreadable operator config is silently treated as first boot | Only ENOENT returns defaults; invalid JSON, non-object JSON and read errors stop hydration while preserving the file. Regression fails before repair and passes afterward. |
| Medium | lib/accounts/rate-limit.ts prunes only expired identifiers but accepts unlimited active keys | Identifier churn can grow the login map without bound | Cap tracked keys, prune expired entries and refuse new keys at capacity without evicting existing blocked identifiers. Regression fails before repair and passes afterward. |
| Medium | README setup requires a missing .env.example and describes the obsolete shared-key auth | Fresh installation instructions fail and operators configure wrong authentication | Add a credential-free example and document account sessions, ADMIN gating and the pinned toolchain. |
| Medium | Readiness workflow only handles PR events and master pushes | Later review-branch commits lack directly triggered verification | Enable push-triggered disposable-PostgreSQL verification for the existing repair branch. |

## Known limitations still requiring evidence

- Paper recovery enforcement remains opt-in. A failed inspection can be advisory until PAPER_RECOVERY_ENFORCE=1 is configured after reconciliation. No trading setting is changed by this audit.
- savePaperLedger and savePersistedConfig log write errors instead of propagating them. Atomic rename protects file shape but is not a verified power-loss recovery guarantee. A bounded durability contract spanning DB, tape, ledger and caller acknowledgments is needed before changing these semantics.
- One API process owns in-memory positions. Multi-process execution is unsupported and can duplicate decisions; preserve single-process operation.
- Some tests remain skipped/quarantined. Counts of passing tests do not establish full feature coverage.
- Historical replay, sustained paper operation and a disposable backup/recovery drill have not been performed in this pass. They remain release gates.
- Container seed files under the volume mount can be obscured by a fresh mounted volume; verify initialization on an empty disposable volume before deploying.
- Build output warns about large dashboard chunks and a source-map location. These are performance/debugging limitations, not failing build gates.

## Validation

Before repair, the saturation and damaged-config regressions failed. After repair, 28 focused tests passed; workspace typechecks and production build passed. Full PostgreSQL CI must be checked on the published follow-up commit. Tests do not touch production state. No deployment or live enablement is performed.

## Rollback

Rollback by selecting the preceding reviewed source commit. Preserve operator config and durable data. A damaged config now stops startup deliberately: repair or restore the backed-up file rather than deleting it to bypass the guard.
