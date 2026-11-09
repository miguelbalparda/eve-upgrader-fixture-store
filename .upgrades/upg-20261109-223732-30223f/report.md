# Upgrade run upg-20261109-223732-30223f

**Site** d46515efa7 (cohort nexcess) · **Mode** upgrade · **Tier** green · **Outcome** verified_green

From **2.4.8-p4** to **2.4.8-p5**. Started 2026-11-09T22:37:32.379Z.

## Verdict

- every critical flow passes as before, no regression, TTFB within budget, no new log lines; host off the supported list for the installed release already (pre-existing migration items recorded, not introduced by this hop); slower only on the cold clone right after the window (graphql(691ms->2321ms)), normal again in the final run

## Stack

PHP 8.3.36, database 10.5.16-MariaDB, search opensearch 2.19.4, composer 2.10.3, magento-community composer, OS CentOS Linux 7 (Core).
composer.lock sha256 before `2586cdab3811947ac8abb66a23b06c4028d24c78440c448df5470b7e835fa26f`, after `0a2cbc3f6aeff2ac9b92e32f3ac9d151fd5f9296968512c1d00b24d9d2386956`.
Patches expected: none.

## Evidence

Upgrade check: verdict 2 (upgrade path ok but needs a server migration), score 57. 2.4.8-p4 -> 2.4.8-p5 works for the code, but this host is not on the supported list: mariadb: 2.4.8-p5 lists mariadb 11.4, 11.8; this host runs 10.5.16 (SELECT VERSION(), already off the 2.4.8-p4 list too); opensearch: 2.4.8-p5 lists opensearch 3; this host runs 2.19.4 (search endpoint, already off the 2.4.8-p4 list too) (the host is already outside the list for the installed release, the target does not change that). Also to prepare: nginx: 2.4.8-p5 lists nginx 1.30; this host runs 1.24.0 (nginx -v, already off the 2.4.8-p4 list too); dev branches: 1 package(s) locked to a dev- branch; a branch deleted upstream makes a full composer update fail (partial updates keep the lock)

| Flow tests | Result | Passed | Regressions | Pre-existing | Slower |
| --- | --- | --- | --- | --- | --- |
| before (baseline) | pass | 14/14 | none | none | none |
| after (closed clone) | pass | 14/14 | none | none | graphql(691ms->2321ms) |
| final (open clone) | pass | 14/14 | none | none | none |

TTFB: baseline 1058 ms, after 1964 ms, budget 2116 ms, within budget.
Log delta: 0 critical, 0 exception lines. Indexers: all indexers valid. Cron: 3 Magento cron line(s) active. Health: see reopen step (health check by the program). Visual diff: not implemented in this version (screenshots need a browser on the clone).
Server run: /chroot/home/a13e1e5c/.magento-upgrade-eve/server-runs/chroot_home_a13e1e5c_d46515efa7.nxcli.io/20261109T223905Z phase awaiting_decision exit 0 store OPEN.

## Phases

| Phase | Status | Seconds | Note |
| --- | --- | --- | --- |
| setup | ok | 14 | programs in /home/a13e1e5c/.magento-upgrade-eve/programs-73a5afd2dfcf (unchanged), allow IP 8.29.157.129,127.0.0.1 |
| baseline-flow-tests | ok | 31 | 14 passed, 0 failed |
| upgrade-check | ok | 13 | verdict 2, score 57, 2.4.8-p4 -> 2.4.8-p5 |
| upgrade-plan | ok | 23 | plan recorded |
| upgrade-to-verify | ok | 434 | clone upgraded to 2.4.8-p5 and CLOSED (server run /chroot/home/a13e1e5c/.magento-upgrade-eve/server-runs/chroot_home_a13e1e5c_d46515efa7.nxcli.io/20261109T223905Z) |
| after-flow-tests | ok | 37 | 14 passed, regressions: none, slower: graphql(691ms->2321ms) |
| deploy-reopen | ok | 16 | clone open on the new release |
| final-flow-tests | ok | 31 | regressions: none |
| promote | running | 0 |  |

## Decisions

No bounded decision was needed.
## Commands

| # | Step | Command | Exit | ms | Output |
| --- | --- | --- | --- | --- | --- |
| 1 | setup | `ensure program dir` | 0 | 897 | commands/001.log |
| 2 | baseline-flow-tests | `mkdir -p '/home/a13e1e5c/.magento-upgrade-eve/runs/upg-20261109-223732-30223f/flows' && bash '/home/a13e1e5c/.magento-up` | 0 | 27174 | commands/002.log |
| 3 | upgrade-check | `bash '/home/a13e1e5c/.magento-upgrade-eve/programs-73a5afd2dfcf/magento-upgrade-check.sh' -r '/home/a13e1e5c/d46515efa7.` | 2 | 9529 | commands/003.log |
| 4 | upgrade-plan | `cd ~ && bash '/home/a13e1e5c/.magento-upgrade-eve/programs-73a5afd2dfcf/magento-patch-upgrade.sh' -r '/home/a13e1e5c/d46` | 0 | 18679 | commands/004.log |
| 5 | upgrade-to-verify | `cd ~ && bash '/home/a13e1e5c/.magento-upgrade-eve/programs-73a5afd2dfcf/magento-patch-upgrade.sh' -r '/home/a13e1e5c/d46` | 0 | 0 | commands/005.log |
| 6 | after-flow-tests | `mkdir -p '/home/a13e1e5c/.magento-upgrade-eve/runs/upg-20261109-223732-30223f/flows' && bash '/home/a13e1e5c/.magento-up` | 0 | 33023 | commands/006.log |
| 7 | deploy-reopen | `cd ~ && bash '/home/a13e1e5c/.magento-upgrade-eve/programs-73a5afd2dfcf/magento-patch-upgrade.sh' --reopen '/chroot/home` | 0 | 13844 | commands/007.log |
| 8 | final-flow-tests | `mkdir -p '/home/a13e1e5c/.magento-upgrade-eve/runs/upg-20261109-223732-30223f/flows' && bash '/home/a13e1e5c/.magento-up` | 0 | 27482 | commands/008.log |
| 9 | post-reads | `cd '/home/a13e1e5c/d46515efa7.nxcli.io' && 'php' bin/magento indexer:status --no-ansi 2>&1 / tail -n 25; echo "__CRON__"` | 0 | 1908 | commands/009.log |

## Pull request

none

## Errors

- log noise: one flow run writes 1 critical and 2 exception lines on this store before any change; raw delta after the hop was 2/4

## Versions

eve 1.0.0-rc.6, ai 7.0.166, zod 4.5.4, ssh2 1.17.0, node v24.22.2, sandbox image eve default image for this eve release.
- magento-patch-upgrade.sh sha256 `724fc396ad4b2bf1d93b8dba1fe6109cbaa4a9d033b43953588d8b0af0753e6c`
- magento-upgrade-check.sh sha256 `732a89fbcaea1616f75837b802ca34c7c51c80007d98883988be5fd2fdfb0fbd`
- magento-audit.sh sha256 `d01ed7f3672fe309572fa939d03db2342e177f8a22dfdcb348ef4769aef46842`
- magento-flow-test.sh sha256 `a12c5a01dddf7aedf404c2285f39a17bdc8657237f6197326229b8a5eeff2c94`

Pointers: report.json /Users/mbalparda/magento2/eve-magento-upgrader/.eve/upgrader/reports/upg-20261109-223732-30223f/report.json, report.md /Users/mbalparda/magento2/eve-magento-upgrader/.eve/upgrader/reports/upg-20261109-223732-30223f/report.md, command logs /Users/mbalparda/magento2/eve-magento-upgrader/.eve/upgrader/reports/upg-20261109-223732-30223f/commands. Agent Runs: search gen_ai.conversation.id or the tool call that returned runId upg-20261109-223732-30223f
