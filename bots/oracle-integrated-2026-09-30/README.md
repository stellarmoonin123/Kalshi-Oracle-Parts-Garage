# Integrated Oracle source — 2026-09-30

GitHub master is `440bd2a4748e9d76771103c0179e576b9ea05b09`, with the exact tested tree `fc6898baa96f23a30aaf50bbb83d082ab0e9ee8f`. The original paper desk remains the deployment target. The 2.1 engine and comparison app are separately packaged; they do not replace the original execution authority.

All 1,587 tracked source files are included, with no runtime configuration, ledger, account database, environment secrets, or node_modules added. The ZIP was verified against every tracked file byte-for-byte and passed its internal integrity check. ZIP parts are concatenated in numeric order, not independently extracted:

```bash
cat complete-source.zip.part??? > complete-source.zip
sha256sum -c SHA256SUMS
unzip complete-source.zip -d source
```

Use the GitHub checkout when executable file modes matter; this archive is a complete tracked-content snapshot. It is split into 15 parts to keep connector uploads reliable.

Merged integrations: #25 (original desk safety), #28 (ARIA, complete API receipts and pre-debit gates), #29 (isolated 2.1 lab/comparison and contributor/foundation guidance). #27 is included through #28. Superseded #5/#6/#14/#19/#21/#23/#24 are closed with provenance in their descriptions. Selected #20 sizing repairs are included; settlement work remains pending. #8 remains explicitly parked, and #22/#26 accounting migrations remain unmerged due acceptance gaps.

Final full CI: 3,396 API passes, zero failures, 498 skips across 453 test files; seven report-guard passes; 382 dashboard passes. The isolated engine passed 182 tests; the comparison workflow passed PostgreSQL isolation, dashboard/login, Docker build and packaged paper smoke checks. Types, schema drift, build and dependency gates passed. Skips are not passing coverage, and CI is not production soak or profitability evidence.

Fly deployment has not been performed. Observed release remains v36. The user elected self-deployment; pause entries, back up volume and database, save the rollback image, deploy the original fly.toml with the full Git SHA, and verify paper mode, identity, health and persisted balances before resuming. No live enablement or threshold increase is authorized by this integration.
