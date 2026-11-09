# Upgrade run upg-20261109-233707-c2a00f

**Site** green-store-github (cohort a-2.4.8) · **Mode** upgrade · **Tier** green · **Outcome** verified_green

From **2.4.8-p4** to **2.4.8-p5**. Started 2026-11-09T23:37:07.840Z.

## Verdict

- every critical flow passes as before, no regression, TTFB within budget, no new log lines

## Stack

PHP 8.3.26, database 10.6.20-MariaDB, search opensearch 2.19.0, composer 2.8.9, magento-community composer, OS AlmaLinux 8.10.
composer.lock sha256 before `e9ed54c79f450c3ea234b07971e5f0745804cfbc9acc7a809ab7aea2495088d8`, after `ffdddde72cbdbe62dfaea3d7fa72961b4c9b861d0a8e6cd09868b0fd581e47ad`.
Patches expected: none.

## Evidence

Upgrade check: verdict 1 (upgrade path ok), score 82. 2.4.8-p4 -> 2.4.8-p5: the target exists and this host meets its requirements

| Flow tests | Result | Passed | Regressions | Pre-existing | Slower |
| --- | --- | --- | --- | --- | --- |
| before (baseline) | pass | 13/13 | none | none | none |
| after (closed clone) | pass | 13/13 | none | none | none |
| final (open clone) | pass | 13/13 | none | none | none |

TTFB: baseline 700 ms, after 700 ms, budget 1500 ms, within budget.
Log delta: 0 critical, 0 exception lines. Indexers: all indexers valid. Cron: 1 Magento cron line(s) active. Health: GET https://clone.example-store.test/ -> 200. Visual diff: not implemented in this version (screenshots need a browser on the clone).
Server run: /home/clone/.magento-upgrade-eve/server-runs/store/20261109-100500 phase awaiting_decision exit ? store OPEN.

## Phases

| Phase | Status | Seconds | Note |
| --- | --- | --- | --- |
| setup | ok | 0 | programs in fixture (unchanged), allow IP 203.0.113.10 |
| baseline-flow-tests | ok | 0 | 13 passed, 0 failed |
| upgrade-check | ok | 0 | verdict 1, score 82, 2.4.8-p4 -> 2.4.8-p5 |
| upgrade-plan | ok | 0 | plan recorded |
| upgrade-to-verify | ok | 9 | clone upgraded to 2.4.8-p5 and CLOSED (server run /home/clone/.magento-upgrade-eve/server-runs/store/20261109-100500) |
| after-flow-tests | ok | 0 | 13 passed, regressions: none, slower: none |
| deploy-reopen | ok | 0 | clone open on the new release |
| final-flow-tests | ok | 0 | regressions: none |
| promote | running | 0 |  |

## Decisions

No bounded decision was needed.
## Commands

| # | Step | Command | Exit | ms | Output |
| --- | --- | --- | --- | --- | --- |
| 1 | baseline-flow-tests | `magento-flow-test.sh --label before (fixture)` | 0 | 1 | commands/001.log |
| 2 | upgrade-check | `magento-upgrade-check.sh (fixture)` | 1 | 1 | commands/002.log |
| 3 | upgrade-plan | `magento-patch-upgrade.sh --plan (fixture)` | 0 | 1 | commands/003.log |
| 4 | upgrade-to-verify | `magento-patch-upgrade.sh --until verify (fixture, detached)` | 0 | 1 | commands/004.log |
| 5 | after-flow-tests | `magento-flow-test.sh --label after (fixture)` | 0 | 1 | commands/005.log |
| 6 | deploy-reopen | `magento-patch-upgrade.sh --reopen (fixture)` | 0 | 1 | commands/006.log |
| 7 | final-flow-tests | `magento-flow-test.sh --label final (fixture)` | 0 | 1 | commands/007.log |

## Pull request

none

## Versions

eve 1.0.0-rc.6, ai 7.0.166, zod 4.5.4, ssh2 1.17.0, node v24.22.2, sandbox image eve default image for this eve release.
- magento-patch-upgrade.sh sha256 `724fc396ad4b2bf1d93b8dba1fe6109cbaa4a9d033b43953588d8b0af0753e6c`
- magento-upgrade-check.sh sha256 `732a89fbcaea1616f75837b802ca34c7c51c80007d98883988be5fd2fdfb0fbd`
- magento-audit.sh sha256 `d01ed7f3672fe309572fa939d03db2342e177f8a22dfdcb348ef4769aef46842`
- magento-flow-test.sh sha256 `a12c5a01dddf7aedf404c2285f39a17bdc8657237f6197326229b8a5eeff2c94`

Pointers: report.json https://sd23igk4ezdklaai.public.blob.vercel-storage.com/magento-upgrader/upg-20261109-233707-c2a00f/report.json, report.md https://sd23igk4ezdklaai.public.blob.vercel-storage.com/magento-upgrader/upg-20261109-233707-c2a00f/report.md, command logs https://sd23igk4ezdklaai.public.blob.vercel-storage.com/magento-upgrader/upg-20261109-233707-c2a00f/commands/. Agent Runs: search gen_ai.conversation.id or the tool call that returned runId upg-20261109-233707-c2a00f
