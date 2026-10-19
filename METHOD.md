An independent user's field report. Not affiliated with Anthropic.

# Method

How the items in this index were found, checked and counted, and what was left out. Counts and method only: no logs are published.

## Sources

Everything comes from the author's own PC and his own sessions:

- the session transcript of one long main session in the Claude desktop app's Code tab;
- the transcripts and journals of the workflow agents that session launched, and each workflow's final run record;
- a running error ledger, written as faults happened;
- daily notes of what was asked and what happened;
- read-only investigations that Claude agents ran afterwards over those records.

Nobody else's logs were used. No network traffic was captured.

## How items were found

1. **Sep 30.** Five sweeps over different kinds of record (notes, the main chat, tool use and workflows among them) produced about 200 candidate items with heavy overlap. They were merged into 74 verified items: 31 about Anthropic products, 8 about other vendors and Windows, and 35 about the author's own process, his scripts and Claude's own mistakes.
2. **Oct 1 to 2.** New faults were added as they happened. The list was written up as a private report to Anthropic and sent on Oct 2, with Claude's own mistakes summarised as behaviour patterns.
3. **Oct 3.** The connection drops and watchdog kills from Oct 1 to 3 were recounted by script (see "Recount it yourself" below). The recount also found faults that were new at the time.
4. **Oct 6.** A census went through every record again, from Sep 19 to Oct 5. It listed each product fault with its first-seen date and where it had been reported, and kept the mistakes of the main Claude session that ran the agents (called the operator in our notes) in a separate list.
5. **This index** starts from that census and the plan for the topic repos. It adds one behaviour case found during the work (FR-60) and leaves out items held back for privacy. On Oct 19 one row was added: FR-62, lines that put the user's name on agents' work.

## How items were checked

- On Sep 30, each kept item was checked against the primary records by an agent that had not written the sweep: the main transcript (streamed, and de-duplicated by record id because the file repeats old records), the agent transcripts and journals, and the files each sweep cited.
- 11 claims were dropped because the records did not support them or contradicted them. Several counts were corrected on the way, for example 12 compactions in the first week, not 5, and 10 refused script paths, not 12.
- The Oct 3 recount was done twice, by a Python standard-library script and a Node standard-library scanner written separately. They agreed exactly on the headline numbers: failed requests, incidents, give-ups, watchdog kills, restarts and lost agents.
- Before each later report went out, separate agents rechecked it claim by claim against its sources.
- Limits of the checking: the checkers were the same model family as the compilers, and no person audited every row against the raw records.

## How items are counted

- **One row per fault.** A later sighting of the same fault adds evidence to that row; it does not add a row.
- **Merged rows.** Three small tool limits are one row (FR-13). The "completed" status and agent starts that never end are one row (FR-03), because both show up in the same run records.
- **Behaviour patterns.** Claude's own mistakes are grouped into seven patterns (FR-55 to FR-60 and FR-62). Each pattern stands for several instances; the instances are not counted.
- **Not counted:** faults in other vendors' tools and in Windows (planned for their own repo), bugs in the author's own code and scripts, and process mistakes that no product change would fix, made by the main Claude session that ran the agents (called the operator in our notes).
- **Held back:** some items are held back for privacy.

## Severity

- **blocker**: lost work or a missed deadline.
- **major**: hours lost, a risky workaround, or a deadline put at risk.
- **minor**: a small cost. **papercut** marks a minor item that was a one-line entry in the private report.

Items with an earlier id keep the rating they were given in the private report where they first appeared. Items with no earlier id were rated for this index from the cost the records show. The ratings reflect this user's work and deadlines, not a measure of how many users are affected.

## Status

Status is as of Oct 6, 2026.

- **public**: a comment with this item's evidence is on an open issue in anthropics/claude-code, posted from the author's account. The four comments were written and posted by a Claude agent through Claude in Chrome on Oct 3, on his yes. Only comments from his account count; an open issue by someone else is listed under related_issues instead.
- **private**: sent to Anthropic through a private channel (the feedback email address or in-app feedback) on the date shown, with no public issue yet.
- **unreported**: no record was found that it was sent anywhere. The author's own sent records were searched; GitHub was not re-searched for this index. A report carrying most of the unreported items was being drafted on Oct 6; the items stay "unreported" here until a send is recorded.

## What was left out, and why

- Raw logs, transcripts, file contents and screenshots, because they hold private details. Only counts and method are published.
- Session ids, request ids and feedback ids. They can be shared with Anthropic privately on request.
- Chat lines. Where a conversation matters, it is paraphrased.
- Local file paths, account details and the names of private people.
- The names of contests and of most third-party tools, replaced with plain descriptions.
- Personal matters.
- Some items, held back for privacy.
- Faults in other vendors' tools (planned for their own repo) and bugs in the author's own code.

## Ids

FR-01 to FR-60 and FR-62 were assigned for this index, in class order; FR-61 is not used yet. The earlier_ids column gives the id each item had in the author's private reports, so Anthropic can match the two. The planned topic repos will use the FR ids.

## Recount it yourself

The headline counts can be recounted from your own Claude Code session transcripts (the .jsonl files in your Claude projects folder). This is the method used here:

1. **Failed requests.** Count records whose subtype is api_error, de-duplicated by uuid, because the transcript can write the same record more than once. Group them by error text.
2. **Incidents and give-ups.** Chain those records by parentUuid. The first record after a chain that is not a system record gives the outcome: an assistant reply means the retry recovered; an assistant record flagged as an API error message means the client gave up.
3. **Hang before a drop.** The gap between two retries, minus the planned wait (retryInMs).
4. **Watchdog kills.** An agent attempt whose last record is the "[Request interrupted by user]" marker, arriving 175 s or more after the record before it. Shorter gaps line up with deliberate stops or app restarts and are left out.
5. **Lost agents.** Agents with state "error" in each workflow's final run record. Attempts that are not named there were restarted.
6. **Images and the watchdog.** An image block, an image inside a tool result, or an image-read note in the last 4 records before the stall. For the base rate, apply the same rule before every model turn that followed a tool result.

The planned session-counter repo will hold standard-library scripts that do this, tested on synthetic fixtures only.

## Licence

This file is part of the field report and is licensed under [CC BY 4.0](LICENSE). Copyright (c) 2026 Devon Fisher.
