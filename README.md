An independent user's field report. Not affiliated with Anthropic.

# Field report 2026

This is the index of every item in one user's field report on Claude Code, the Claude desktop app and Claude in Chrome, collected on Windows from late September to early October 2026. Each item is one fault, limit or behaviour pattern. Each row gives its severity, the date it was first seen, where it happened, and whether it has been reported publicly.

- [ITEMS.md](ITEMS.md): the full list, to read.
- [ITEMS.csv](ITEMS.csv): the same list, to sort and filter.
- [METHOD.md](METHOD.md): how the items were found, checked and counted, and what was left out.

## At a glance

Status as of Oct 6, 2026.

| | Items |
|---|---|
| All items | **60**, in 8 classes |
| Reported publicly (a comment on an open GitHub issue) | 5 |
| Sent to Anthropic privately, with no public issue yet | 44 |
| Not reported anywhere yet | **11** |
| Rated blocker / major / minor | 3 / 29 / 28 |

Recount the headline numbers on your own logs with [session-counter](https://github.com/devonmvfisher/session-counter). On the author's Oct 1 to 3 logs it reproduces 208 failed requests in 54 incidents, 353 watchdog kills and 39 lost agents.

| Class | Items | Public | Private only | Unreported |
|---|---|---|---|---|
| [Workflow runtime](ITEMS.md#workflow-runtime) | 13 | 5 | 8 | 0 |
| [API drops and retries](ITEMS.md#api-drops-and-retries) | 6 | 0 | 3 | 3 |
| [Memory, rules and instructions](ITEMS.md#memory-rules-and-instructions) | 7 | 0 | 4 | 3 |
| [Continuity (restarts and retention)](ITEMS.md#continuity-restarts-and-retention) | 7 | 0 | 5 | 2 |
| [Desktop app papercuts](ITEMS.md#desktop-app-papercuts) | 9 | 0 | 9 | 0 |
| [Claude in Chrome](ITEMS.md#claude-in-chrome) | 8 | 0 | 6 | 2 |
| [Auto mode and safeguards](ITEMS.md#auto-mode-and-safeguards) | 4 | 0 | 4 | 0 |
| [Model behaviour](ITEMS.md#model-behaviour) | 6 | 0 | 5 | 1 |

The five public items are comments on [#88993](https://github.com/anthropics/claude-code/issues/88993) (the 180 s watchdog, and the retry that resends a completed call), [#94012](https://github.com/anthropics/claude-code/issues/94012) ("completed" with failed agents), [#96640](https://github.com/anthropics/claude-code/issues/96640) (the chat message relayed into agents) and [#87140](https://github.com/anthropics/claude-code/issues/87140) (one Stop ends every agent), all posted Oct 3, 2026. Five items sit on four issues because FR-01 and FR-02 share #88993.

## Who wrote it

Devon Fisher ([devonmvfisher](https://github.com/devonmvfisher) on GitHub), an independent user of Claude Code. He is not affiliated with Anthropic.

Every item comes from his own local records of his own sessions. Claude (Opus 5.5) agents running in the same setup helped find, check and count the items and drafted these files; he reviews and publishes them. So the model that compiled this report is also the model some of its items describe. Please read the framing with that in mind, in both directions.

## Environment

- Windows 11 Home (build 10.0.26200, x64). One main PC; a second PC appears in one item (FR-33).
- Claude desktop app, Code tab: version 2.9939.2.0 on Sep 30 and 2.16120.0.0 on Oct 3.
- Claude Code 2.1.281 (to Oct 1), 2.1.284 (Oct 1 to 3), and 2.1.286 when read on Oct 6.
- Model Opus 5.5, auto mode on, effort xhigh.
- The Claude in Chrome extension in Google Chrome.
- Typical use: one long main session, often near 900k tokens of context, with many background workflows (multi-agent scripts) running at the same time.

## How items are counted

- One row per fault. When a fault was seen again later, the new evidence went into its row; it did not make a new row.
- Three small tool limits share one row (FR-13).
- Claude's own mistakes are grouped into six behaviour patterns (FR-55 to FR-60), not listed one by one.
- Faults in other vendors' tools, and bugs in the author's own scripts, are not counted here.
- Some items are held back for privacy.

The details are in [METHOD.md](METHOD.md).

## How to read the table

| Column | Meaning |
|---|---|
| id | FR-01 to FR-60, assigned for this index, in class order. The topic repos will use the same ids. |
| class | One of 8 groups. Each group has a planned topic repo. |
| description | One line in plain words. Numbers in brackets are counts from the author's own logs. |
| severity | **blocker**: lost work or a missed deadline. **major**: hours lost, a risky workaround, or a deadline put at risk. **minor**: a small cost. **papercut**: a one-line minor item. |
| first_seen | The date the author first saw it, in US Central time. "(or earlier)" means it had already happened by that date. |
| environment | Where it happened, within the setup above. |
| status | **public**: the author commented on that open issue in anthropics/claude-code, on the date shown. **private**: sent to Anthropic through a private channel on the date shown, with no public issue yet. **unreported**: not sent anywhere yet. |
| topic_repo | The planned repo that will hold the full write-up. None is published yet. |
| earlier_ids | The id the item had in the author's earlier private reports to Anthropic, so the two can be matched. "none" if it had no earlier id. |
| related_issues | Open issues by other people that look like the same fault, noted on Oct 2 and 3, 2026 and not re-checked since. |

## Topic repos (planned)

Each class gets its own repo with the full write-up of its items: what happens, steps, expected and actual, cost, workaround, and the ask. The names are proposals.

| Repo | Scope | Status |
|---|---|---|
| field-report-2026 | This index: every item, its status, and the method. | this repo |
| workflow-agent-bugs | Workflow runtime faults: the 180 s watchdog, the retry that resends a paid call, "completed" over failed agents, one Stop ends all, relayed chat, parallel copies, refused script paths. | not yet published |
| [session-counter](https://github.com/devonmvfisher/session-counter) | Standard-library counters (Python and Node) that recount failed requests, give-ups, watchdog kills and lost agents from your own local logs. Synthetic fixtures only. | published |
| api-drops-report | Connection drops and retry chains: counts, the timeline method, messages that wait behind a retry chain, no restart after a give-up, and the correction that drops do not follow context size. | not yet published |
| rules-that-dont-fire | Rules that live only in memory files fail mid-session, the working method is lost after a compaction, and nothing shows what is loaded. | not yet published |
| desktop-continuity-report | Restarts and retention: workflows and monitors lost at a restart, unsent drafts lost, outputs gone, 30-day transcript deletion without notice, phone file limits. | not yet published |
| desktop-papercuts | Small desktop app faults: the Cowork VM, folded text, Browser pane focus theft, agent tabs left open, file:// pages, the usage card label. | not yet published |
| browser-agent-field-notes | Claude in Chrome: frozen-tab timeouts, tab groups, the "Draft saved" that was not saved, the debugging banner on the user's own tab, clicks reported as done with no effect, disconnects. | not yet published |
| refusals-without-a-rule | Auto-mode and safeguard stops that name no rule, with dates, and one ask: name the rule. | not yet published |
| model-behaviour-notes | Claude's own mistakes as patterns, paraphrased, with no chat lines. | not yet published |
| other-vendor-field-notes | Faults met in other vendors' tools while running this setup. Not part of the Anthropic set, so not counted in this index. | not yet published |

session-counter is a tool, so it has no rows here. It is how anyone can check the counts against their own logs.

## Honest limits

- One user, one setup, one operating system (Windows 11), over a few weeks in September and October 2026.
- Several items were seen only once; their rows say so.
- Severity reflects this user's work and deadlines. Items with an earlier id keep the rating they had in the private report; items without one were rated for this index.
- Every count comes from the author's own local logs. Nobody else's logs were checked. The session transcript repeats some records, so counts were de-duplicated first (FR-20).
- From these logs a dropped connection cannot be told apart from a fault in the user's own network (FR-14, FR-17).
- The related issue numbers were not re-checked for this index.
- Status can change after Oct 6, 2026. This index is not updated automatically, and newer app versions may already fix some items.
- Nothing here is a statement by Anthropic.

Session, request and feedback ids behind the counts are not published. They can be shared with Anthropic privately on request.

## Licence

The text and data in this repository are licensed under [CC BY 4.0](LICENSE). Copyright (c) 2026 Devon Fisher.
