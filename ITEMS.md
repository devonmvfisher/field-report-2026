An independent user's field report. Not affiliated with Anthropic.

# Items

Every item in the field report, one row each: 61 items in 8 classes, status as of 2026-10-06. The same rows, with the class and planned topic repo on every row, are in [ITEMS.csv](ITEMS.csv). How to read the columns: [README.md](README.md#how-to-read-the-table). How items were found and counted: [METHOD.md](METHOD.md).

## Totals

| Class | Planned topic repo (not yet published) | Items | Public | Private only | Unreported |
|---|---|---|---|---|---|
| [Workflow runtime](#workflow-runtime) | workflow-agent-bugs | 13 | 5 | 8 | 0 |
| [API drops and retries](#api-drops-and-retries) | api-drops-report | 6 | 0 | 3 | 3 |
| [Memory, rules and instructions](#memory-rules-and-instructions) | rules-that-dont-fire | 7 | 0 | 4 | 3 |
| [Continuity (restarts and retention)](#continuity-restarts-and-retention) | desktop-continuity-report | 7 | 0 | 5 | 2 |
| [Desktop app papercuts](#desktop-app-papercuts) | desktop-papercuts | 9 | 0 | 9 | 0 |
| [Claude in Chrome](#claude-in-chrome) | browser-agent-field-notes | 8 | 0 | 6 | 2 |
| [Auto mode and safeguards](#auto-mode-and-safeguards) | refusals-without-a-rule | 4 | 0 | 4 | 0 |
| [Model behaviour](#model-behaviour) | model-behaviour-notes | 7 | 0 | 5 | 2 |
| **All 8 classes** | | **61** | **5** | **44** | **12** |

By severity: blocker 3, major 30, minor 28 (10 of the minor items are papercuts).

## Workflow runtime

Planned topic repo: `workflow-agent-bugs` (not yet published). 13 items.

| ID | What happens | Severity | First seen | Environment | Status | Earlier id | Related open issues |
|---|---|---|---|---|---|---|---|
| FR-01 | The stall watchdog kills a workflow agent 180 s after a tool result returns, while it waits for the model's next turn, then restarts it from an empty transcript, up to 6 times (353 kills from Oct 1 to 3; 285 had an image just before the stall). | blocker | 2026-09-26 (or earlier) | Windows 11; desktop app Code tab; workflow agents | public: anthropics/claude-code [#88993](https://github.com/anthropics/claude-code/issues/88993) (comment, 2026-10-03) | CC-1 | [#88993](https://github.com/anthropics/claude-code/issues/88993), [#90092](https://github.com/anthropics/claude-code/issues/90092), [#63698](https://github.com/anthropics/claude-code/issues/63698) |
| FR-02 | A watchdog retry starts cold and can resend a tool call that had already completed, including a paid generation request (identical requests found 3 times in one run and once in another). | major | 2026-09-29 | Windows 11; desktop app Code tab; workflow agents | public: anthropics/claude-code [#88993](https://github.com/anthropics/claude-code/issues/88993) (inside the watchdog comment, 2026-10-03) | CC-15 | [#88993](https://github.com/anthropics/claude-code/issues/88993), [#91449](https://github.com/anthropics/claude-code/issues/91449) |
| FR-03 | A workflow reports "completed" while some of its agents ended in error, and its journal can hold agent starts that never end and never appear in the run record (12 runs hid 39 failed agents; 45 such starts in 9 more runs). | major | 2026-09-27 | Windows 11; desktop app Code tab; workflow agents | public: anthropics/claude-code [#94012](https://github.com/anthropics/claude-code/issues/94012) (comment, 2026-10-03) | CC-3 | [#94012](https://github.com/anthropics/claude-code/issues/94012), [#93270](https://github.com/anthropics/claude-code/issues/93270) |
| FR-04 | One Stop or Esc during a main-chat turn ends every background workflow agent and shell (4 agents in 2 unrelated runs ended in the same second). | major | 2026-09-28 | Windows 11; desktop app Code tab; workflow agents | public: anthropics/claude-code [#87140](https://github.com/anthropics/claude-code/issues/87140) (comment, 2026-10-03) | CC-2 | [#87140](https://github.com/anthropics/claude-code/issues/87140) |
| FR-05 | The user's latest chat message is appended to every new workflow agent as a request that outranks its script (387 agents in 35 runs over two days); one agent told to ignore it acted on it. | major | 2026-09-27 | Windows 11; desktop app Code tab; workflow agents | public: anthropics/claude-code [#96640](https://github.com/anthropics/claude-code/issues/96640) (comment, 2026-10-03) | CC-4 | [#96640](https://github.com/anthropics/claude-code/issues/96640), [#95369](https://github.com/anthropics/claude-code/issues/95369), [#97076](https://github.com/anthropics/claude-code/issues/97076) |
| FR-06 | SendMessage to a running workflow agent starts a second, parallel copy of it instead of queuing the message. | major | 2026-09-26 | Windows 11; desktop app Code tab; workflow agents | private: sent to Anthropic on 2026-10-02; no public issue | CC-5 |  |
| FR-07 | The Workflow tool refuses a script path it returned itself once the session's working folder has moved; one change-directory command inside a Bash call is enough (10 refusals in 5 days). | major | 2026-09-26 | Windows 11; desktop app Code tab; workflow agents | private: sent to Anthropic on 2026-10-02; no public issue | CC-6 |  |
| FR-08 | Subagents are refused when they write the report file their workflow script names, so the result exists only in task output and can be missed. | minor | 2026-09-26 | Windows 11; desktop app Code tab; workflow agents | private: sent to Anthropic on 2026-10-02; no public issue | CC-8 | [#81475](https://github.com/anthropics/claude-code/issues/81475), [#44657](https://github.com/anthropics/claude-code/issues/44657) |
| FR-09 | An agent that dies on an API error (DNS failure, ECONNRESET, HTTP 408) is never retried, although a stalled agent is (9 review agents lost on Oct 3). | minor | 2026-09-26 | Windows 11; desktop app Code tab; workflow agents | private: sent to Anthropic on 2026-10-02; no public issue | CC-16 |  |
| FR-10 | Stopping a workflow leaves the child processes it started still running and holding memory. | minor | 2026-09-27 | Windows 11; desktop app Code tab; workflow agents | private: sent to Anthropic on 2026-10-02; no public issue | CC-10 |  |
| FR-11 | Agents keep retrying a foreground sleep that the harness blocks by design (23 blocks in one run). | minor | 2026-10-02 (or earlier) | Windows 11; desktop app Code tab; workflow agents | private: sent to Anthropic on 2026-10-02; no public issue | CC-14 |  |
| FR-12 | A valid workflow script was rejected for hidden control characters that a scan did not find. | minor (papercut) | 2026-09-29 | Windows 11; desktop app Code tab; workflow agents | private: sent to Anthropic on 2026-10-02; no public issue | CC-11 |  |
| FR-13 | Small tool limits cause retries: searches time out at 20 s on large folders, Read caps a file at 25k tokens, and one research session ran out of web search budget. | minor (papercut) | 2026-09-24 | Windows 11; desktop app Code tab | private: sent to Anthropic on 2026-10-02; no public issue | CC-13; CC-17; CC-19 |  |

## API drops and retries

Planned topic repo: `api-drops-report` (not yet published). 6 items.

| ID | What happens | Severity | First seen | Environment | Status | Earlier id | Related open issues |
|---|---|---|---|---|---|---|---|
| FR-14 | Main-chat requests hang, drop with "Connection dropped (ECONNRESET)" and retry up to 10 times with only a counter on screen (208 failed requests in 54 incidents, Oct 1 to 3); later counts show the drops do not follow context size. | blocker | 2026-09-29 | Windows 11; desktop app Code tab; main chat | private: sent to Anthropic on 2026-10-02; no public issue | APP-1 | [#87757](https://github.com/anthropics/claude-code/issues/87757), [#90235](https://github.com/anthropics/claude-code/issues/90235), [#87424](https://github.com/anthropics/claude-code/issues/87424) |
| FR-15 | After 10 failed retries the turn ends with an API error and the reply is lost (7 give-ups from Oct 1 to 3, 3 more on Oct 4). | major | 2026-10-01 | Windows 11; desktop app Code tab; main chat | private: sent to Anthropic on 2026-10-02; no public issue | APP-11 | [#87757](https://github.com/anthropics/claude-code/issues/87757) |
| FR-16 | Nothing restarts after a give-up, and a message typed during a retry chain waits until the chain ends (one waited 35 minutes). | major | 2026-10-02 | Windows 11; desktop app Code tab; main chat | unreported | none |  |
| FR-17 | Retry state is not logged: the retry counter and the "Connection problem" screen leave no record, and agent transcripts hold no retry records, so a stalled agent cannot be told from a retrying one. | major | 2026-10-03 | Windows 11; desktop app Code tab | unreported | none |  |
| FR-18 | Workflow agents failed on HTTP 401 errors while the login was valid, in a cluster as Cowork opened in the same app. | major | 2026-09-27 | Windows 11; desktop app Code tab; workflow agents | private: sent to Anthropic on 2026-10-02; no public issue | CC-7 |  |
| FR-19 | HTTP 400 "Could not process image" on a pasted PNG screenshot; the same image sent as JPEG read fine (seen once). | minor | 2026-10-02 | Windows 11; desktop app Code tab; main chat | unreported | none |  |

## Memory, rules and instructions

Planned topic repo: `rules-that-dont-fire` (not yet published). 7 items.

| ID | What happens | Severity | First seen | Environment | Status | Earlier id | Related open issues |
|---|---|---|---|---|---|---|---|
| FR-20 | Compaction near 900k tokens blocks the chat for 2 to 11 minutes, and the session transcript writes some records up to 3 times (16,743 of 50,840 records were repeats), which inflates any count taken from it. | major | 2026-09-25 | Windows 11; desktop app Code tab; main chat | private: sent to Anthropic on 2026-10-02; no public issue | MEM-1 |  |
| FR-21 | A compaction summary keeps the task list but drops the working method: installed skills, tools built in the session, and how work is checked. | minor | 2026-09-26 | Windows 11; desktop app Code tab; main chat | private: sent to Anthropic on 2026-10-02; no public issue | MEM-2 |  |
| FR-22 | No panel or command shows which rules and memory files are loaded for the session or for an agent, or what is reread after a compaction (a Claude agent counted 14 breaks of the setup's own rules by the main Claude session in 2 days, from the user's complaints and the error ledgers). | major | 2026-10-04 | Windows 11; desktop app Code tab | unreported | none |  |
| FR-23 | Agents break a hard rule printed in their prompt about 1 time in 3 and rarely say so (311 of 974 agents that used Bash ran a forbidden change-directory command; no harm found). | minor | 2026-10-02 | Windows 11; desktop app Code tab; workflow agents | unreported | none |  |
| FR-24 | A user skill created during a session answered "Unknown skill" 3.5 hours later in the same session. | minor (papercut) | 2026-09-29 | Windows 11; desktop app Code tab | private: sent to Anthropic on 2026-10-02; no public issue | MEM-3 |  |
| FR-25 | Harness flags are noisy: an "instruction-shaped pattern" prefix on agent results that quote settings text, and a shared-scratchpad flag. | minor (papercut) | 2026-09-27 | Windows 11; desktop app Code tab; workflow agents | private: sent to Anthropic on 2026-10-02; no public issue | CC-12 |  |
| FR-26 | The model cannot start a compaction itself, even with the user's yes, so long runs need the user present first (by design; a feature request). | minor | 2026-09-25 | Windows 11; desktop app Code tab | unreported | none |  |

## Continuity (restarts and retention)

Planned topic repo: `desktop-continuity-report` (not yet published). 7 items.

| ID | What happens | Severity | First seen | Environment | Status | Earlier id | Related open issues |
|---|---|---|---|---|---|---|---|
| FR-27 | An app restart or a crash ends every running workflow and background shell, with no park or resume (seen Sep 27, Sep 28, Oct 1 and Oct 4). | major | 2026-09-27 | Windows 11; desktop app | private: sent to Anthropic on 2026-10-02; no public issue | APP-3 |  |
| FR-28 | Unsent prompt drafts are lost on restart, and the window went blank under memory pressure with no way to reload it. | major | 2026-09-27 | Windows 11; desktop app | private: sent to Anthropic on 2026-10-02; no public issue | APP-4 |  |
| FR-29 | Local session transcripts are deleted after 30 days by default, with no notice in the desktop app (two months of records were gone from one PC). | major | 2026-10-05 | Windows 11; desktop app | unreported | none |  |
| FR-30 | Workflow outputs from before an app restart are gone and only the journals survive (49 of 183 runs). | minor | 2026-09-27 | Windows 11; desktop app Code tab; workflow agents | private: sent to Anthropic on 2026-10-02; no public issue | CC-9 |  |
| FR-31 | Files of about 0.9 MiB and up fail to reach the phone through Remote Control (30 s timeout). | minor | 2026-09-28 | Windows 11; desktop app; Remote Control on a phone | private: sent to Anthropic on 2026-10-02; no public issue | APP-8 |  |
| FR-32 | After a restart the screen said comment monitors did not resume while the saved record listed 4 armed (seen once). | minor | 2026-10-04 | Windows 11; desktop app | unreported | none |  |
| FR-33 | A desktop session on one PC cannot be opened or viewed from a second PC signed in to the same account. | minor | 2026-10-02 (or earlier) | Windows 11; two PCs; desktop app | private: sent to Anthropic on 2026-10-02; no public issue | none |  |

## Desktop app papercuts

Planned topic repo: `desktop-papercuts` (not yet published). 9 items.

| ID | What happens | Severity | First seen | Environment | Status | Earlier id | Related open issues |
|---|---|---|---|---|---|---|---|
| FR-34 | The Cowork VM reserves 4 GiB while the process list shows under 100 MB, retries every 5 minutes, has no off switch, and stopping it by force restarts the whole app. | major | 2026-09-27 | Windows 11; desktop app | private: sent to Anthropic on 2026-10-02; no public issue | APP-2 |  |
| FR-35 | Text written before a tool call folds into a one-line summary in the default view, so steps addressed to the user go unseen. | major | 2026-09-27 (or earlier) | Windows 11; desktop app Code tab | private: sent to Anthropic on 2026-10-02; no public issue | APP-5 |  |
| FR-36 | The usage card shows a per-model weekly row beside the all-models row with no sign that it is a sub-limit of it. | major | 2026-10-03 | Windows 11; desktop app | private: sent to Anthropic on 2026-10-04; no public issue | none |  |
| FR-37 | The Browser pane takes keyboard focus when an agent navigates it, so the user's chat typing lands in its URL bar (whether Enter then submits the text was not tested). | minor | 2026-10-02 | Windows 11; desktop app Code tab | private: sent to Anthropic on 2026-10-02; no public issue | APP-12 |  |
| FR-38 | PushNotification skips the phone push while the Claude window has focus. | minor | 2026-09-26 | Windows 11; desktop app; Remote Control on a phone | private: sent to Anthropic on 2026-10-02; no public issue | APP-6 | [#93997](https://github.com/anthropics/claude-code/issues/93997), [#87549](https://github.com/anthropics/claude-code/issues/87549) |
| FR-39 | An unasked "(fork)" copy of the session appeared in the session list (seen once). | minor (papercut) | 2026-09-27 | Windows 11; desktop app | private: sent to Anthropic on 2026-10-02; no public issue | APP-7 |  |
| FR-40 | Two built-in tools disappear for 21 to 68 seconds after every app restart. | minor (papercut) | 2026-09-27 | Windows 11; desktop app | private: sent to Anthropic on 2026-10-02; no public issue | APP-9 |  |
| FR-41 | An agent cannot open a local file:// page in the Browser pane (13 times). | minor (papercut) | 2026-09-30 (or earlier) | Windows 11; desktop app Code tab | private: sent to Anthropic on 2026-10-02; no public issue | APP-10 |  |
| FR-42 | Browser pane tabs opened by agents stay open after the agents finish; one kept looping a video with sound. | minor (papercut) | 2026-10-01 | Windows 11; desktop app Code tab | private: sent to Anthropic on 2026-10-02; no public issue | APP-13 |  |

## Claude in Chrome

Planned topic repo: `browser-agent-field-notes` (not yet published). 8 items.

| ID | What happens | Severity | First seen | Environment | Status | Earlier id | Related open issues |
|---|---|---|---|---|---|---|---|
| FR-43 | A Gmail draft written in a background tab showed "Draft saved" but never reached Drafts, and typed text did not reach the compose body. | major | 2026-10-02 | Windows 11; Chrome with the Claude in Chrome extension | private: sent to Anthropic on 2026-10-02; no public issue | CHR-7 |  |
| FR-44 | The extension disconnects ("not connected" 3 times) and its side panel falls back to the first-run screen until the user clicks through it again. | major | 2026-10-03 | Windows 11; Chrome with the Claude in Chrome extension | unreported | none |  |
| FR-45 | Clicks and typed text come back as done with no effect on the page, and no error is logged (a new-repository page ignored the first two clicks). | major | 2026-10-04 | Windows 11; Chrome with the Claude in Chrome extension | unreported | none |  |
| FR-46 | Screenshots and page actions time out on heavy or background tabs ("renderer may be frozen"). | minor | 2026-09-27 | Windows 11; Chrome with the Claude in Chrome extension | private: sent to Anthropic on 2026-10-02; no public issue | CHR-2 |  |
| FR-47 | A form submit that navigates puts the tab outside Claude's tab group. | minor | 2026-09-27 | Windows 11; Chrome with the Claude in Chrome extension | private: sent to Anthropic on 2026-10-02; no public issue | CHR-3 |  |
| FR-48 | Chrome showed its "started debugging this browser" banner on the user's own upload tab during an agent's session; whether the agent acted on that tab is not settled. | minor (provisional; major if the agent acted on that tab) | 2026-10-01 | Windows 11; Chrome with the Claude in Chrome extension | private: sent to Anthropic on 2026-10-02; no public issue | CHR-8 |  |
| FR-49 | A code-hosting settings form ignored typed input and form_input, so the user changed the setting by hand. | minor (papercut) | 2026-09-28 | Windows 11; Chrome with the Claude in Chrome extension | private: sent to Anthropic on 2026-10-02; no public issue | CHR-4 |  |
| FR-50 | An upload was refused for a file in a synced folder because the session had not read that file first. | minor (papercut) | 2026-09-29 | Windows 11; Chrome with the Claude in Chrome extension | private: sent to Anthropic on 2026-10-02; no public issue | CHR-6 |  |

## Auto mode and safeguards

Planned topic repo: `refusals-without-a-rule` (not yet published). 4 items.

| ID | What happens | Severity | First seen | Environment | Status | Earlier id | Related open issues |
|---|---|---|---|---|---|---|---|
| FR-51 | The auto-mode classifier blocks routine steps (false positives such as car photos flagged as personal data) and sometimes gives no verdict; 7 more subagent denials on Oct 2 and 3, at least 3 of them false positives. | major | 2026-09-25 | Windows 11; desktop app Code tab; auto mode | private: sent to Anthropic on 2026-10-02; no public issue | PERM-1 |  |
| FR-52 | Commit-type steps the user asked for (an upload, a form submit) are blocked until the user types a yes, with no approve-once option. | major | 2026-10-02 (or earlier) | Windows 11; Claude in Chrome; auto mode | private: sent to Anthropic on 2026-10-02; no public issue | PERM-2 |  |
| FR-53 | Two safeguard stops and one content-filter error ended creative work with no reason and no retry; one stop may have been fair, and the ask is a reason and a way to revise. | major | 2026-09-29 | Windows 11; desktop app Code tab | private: sent to Anthropic on 2026-10-02; no public issue | PERM-3 |  |
| FR-54 | Auto-mode refusals name no rule: a workflow launch refused with no explanation (it would have had agents drive two web apps whose terms ban automated use, as agents had already done there on Sep 29 and 30 without a block; it was relaunched with those steps moved to the user's own clicks), an agent blocked from re-reading a page, and a push to the user's own repository and a restart of the user's own script refused, the same restart allowed 2 hours earlier. | minor | 2026-10-02 | Windows 11; desktop app Code tab; auto mode | private: the Oct 2 workflow-launch case and the ask to name the rule were sent to Anthropic on 2026-10-03; the later cases are not yet sent; no public issue | none |  |

## Model behaviour

Planned topic repo: `model-behaviour-notes` (not yet published). 7 items.

| ID | What happens | Severity | First seen | Environment | Status | Earlier id | Related open issues |
|---|---|---|---|---|---|---|---|
| FR-55 | Under a stated deadline, the requested item did not come first: side tasks ran before it. | blocker | 2026-09-30 | Opus 5.5; desktop app Code tab | private: sent to Anthropic on 2026-10-02; no public issue | OWN-1 |  |
| FR-56 | Status and readiness were claimed without tool output behind them, such as work called checked while its reviewers had returned nothing. | major | 2026-09-27 | Opus 5.5; desktop app Code tab | private: sent to Anthropic on 2026-10-02; no public issue | OWN-2 |  |
| FR-57 | A risk or a cause was stated from assumption, such as a forced VM stop called low risk and stalls blamed on long tool calls. | major | 2026-09-28 | Opus 5.5; desktop app Code tab | private: sent to Anthropic on 2026-10-02; no public issue | OWN-3 |  |
| FR-58 | Caveats and capabilities were lost between research, summaries and compactions, such as a tool built in the session being forgotten. | major | 2026-09-26 | Opus 5.5; desktop app Code tab | private: sent to Anthropic on 2026-10-02; no public issue | OWN-4 |  |
| FR-59 | Heavy or unsettled work was launched without checks, such as parallel jobs pushing memory to 97 to 99% and agents using the browser during the user's own upload. | major | 2026-09-27 | Opus 5.5; desktop app Code tab | private: sent to Anthropic on 2026-10-02; no public issue | OWN-5 |  |
| FR-60 | A visual claim was made from expectation: a clock face with one hand and no numerals was read as the exact time the plan asked for, and a check that knew the plan passed it. | major | 2026-10-01 | Opus 5.5; desktop app Code tab | unreported | none |  |
| FR-62 | Text Claude wrote put the user's name on work agents did: four GitHub issue comments in his first person, written and posted by an agent from his account (Oct 3); a contest bio that voiced Claude's opinions as his (Sep 30); this index's own line that he reviews the files (Oct 6); and orders for other agents written in his voice ('my own words'), after which one agent wrote that he had authorized its changes (Oct 7). | major | 2026-09-30 | Opus 5.5; desktop app Code tab; workflow agents | unreported | none |  |

Related open issues were noted from searches of the public tracker made on Oct 2 and 3, 2026, and were not re-checked for this index. Where a status says public, a comment was posted on that issue from the author's account (written and posted by a Claude agent on his yes, Oct 3).
