---
name: build-handoff-and-retest
description: Use when handing over a build or fix for review, or when retesting a reported bug after a fix. Gives the exact fields a handoff needs and the retest steps before an issue can be called fixed.
---

# Build handoff and retest

## Handoff (what you hand back)
- What changed, and which acceptance criteria it addresses.
- Source revision and branch. Say if anything uncommitted affects the build.
- Artifact filename, link, hash, build time.
- Platform and how to launch it. Starting state or test data needed.
- Checks run and their results. Checks never run, listed as "never run".
- Label all of this "Cliff-reported" (or the bot's name). It is not independent.

## Combined builds
If the build bundles several unmerged branches, list each fix expected in it. Before handing
over, confirm each fix is actually present (not just that the build compiled). A build from
one branch silently drops every other unmerged fix.

## Retest a reported bug
1. Get the new build's exact identity (revision or hash). If it cannot be pinned, say so; do not
   claim the exact version was checked.
2. Repeat the ORIGINAL reproduction steps on that build.
3. Check the nearby behaviour that the fix could have broken.
4. Record the failed run and the passing run as separate dated results.
5. Close the issue only after the retest passes, or Kate explicitly defers it.

## Status words (use only these)
queued, implementing, ready for review, fixes requested, verified, blocked.
- "Implemented" is not "verified". Built is not launched. Launched is not exercised.
- A screenshot shows state, not behaviour. Do not infer behaviour from a still.
- Blocked or never-run required checks do not count as passes.

## Reporting a failure
Criterion, exact build, starting state, minimal steps, expected vs actual, how often, and the
evidence. Label suspected causes as hypotheses.

## Authority
Merging, publishing, deploying, spending and account changes need Kate's explicit approval.
