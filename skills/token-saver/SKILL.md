---
name: token-saver
description: Use when someone asks to save tokens, be token efficient, watch context, go easy on context usage, or reduce token/context burn — a discipline layer for keeping conversations and multi-step work lean. Also apply proactively any time a request risks unnecessary token spend (dumping a whole file when a search would do, carrying a full transcript into a subagent, producing more output than was asked for).
---

## Companion: caveman output style

When this skill activates, also apply the `caveman` skill's **full** output style for the
rest of the session (terse, no filler, technical substance intact) — unless Kate has already
set a different caveman level or said "stop caveman"/"normal mode" this session, in which case
leave her setting alone. This skill governs *behavior* (what work to do/skip); caveman governs
*prose* (how replies are worded) — token-saver invoking it just saves Kate from typing both.

## What This Skill Does

Applies a checklist of token-saving habits during the current session, adapted from the
"level 1" rules in Nate B Jones' *"Paste This Into Claude, Never Hit a Token Limit Again"*
(the 10 of his 15 rules that are pure workflow discipline, not ones requiring a proxy that
intercepts requests before they reach the model — that part is architecturally out of reach
for a skill and isn't attempted here).

This is **active and visible**: when a moment triggers one of these, say so briefly before
proceeding, not just silently comply. One flag per relevant moment — don't repeat the same
flag every message, and don't gatekeep genuinely large/thorough work Kate actually wants.

## The checklist

1. **Edit-in-place, not "that was wrong."** If Kate corrects or redirects a request she just
   made, note once that editing and resending the previous message is cheaper than a fresh
   correction turn — it avoids paying for the wrong answer twice. Say it once per session at
   most; this is a habit for her to build, not something Claude can enforce directly.

2. **Batch related questions, name the output shape.** Don't trickle clarifying questions
   across separate turns — batch them (this is already how `AskUserQuestion` should be used).
   When a request doesn't specify length/format, ask or default to concise rather than
   guessing large.

3. **Flag a session boundary when the topic pivots.** If the conversation clearly moves to an
   unrelated task, say so and suggest a fresh session rather than silently dragging
   accumulated context into work that doesn't need it.

4. **Carry the result forward, not the argument.** When handing work between stages or
   subagents (research → plan → build), pass the distilled artifact or conclusion in the next
   prompt — not the full prior transcript, reasoning trail, rejected drafts, or debate that
   produced it.

5. **Match output size to what was asked.** Default to concise. Don't produce more than the
   request calls for — extra output costs twice: once to generate, again every time it's
   carried forward as input on later turns.

6. **Search before you read.** Grep or target a specific section before opening a large file
   wholesale; use `offset`/`limit` rather than reading files end-to-end when only part is
   relevant.

7. **Send the lightest useful form of a source.** When only the text content matters (not
   layout), prefer extracted text/markdown over repeatedly re-reading a PDF, screenshot, or
   other heavy format.

8. **Don't redo work already done this session.** *(Inferred — the source video's rule 8 was
   lost to a caption gap, so this is a best-guess fill, not confirmed Nate B Jones content.)*
   If something was already fetched, read, or derived earlier in the conversation, reuse it
   instead of re-fetching or re-deriving it.

9. **Point recurring answers at a durable store.** If the same fact or result would otherwise
   get re-derived across sessions, put it somewhere retrievable (memory, notes, a wiki) instead
   of re-computing it each time it's needed.

10. **Load tools deliberately.** Don't reach for a heavy subagent, broad tool search, or wide
    MCP surface for a small task — match the weight of what gets invoked to the size of the
    job. A quick lookup doesn't need a research agent; a targeted grep doesn't need a full
    Explore pass.

## What this skill does NOT do

Rules from the source video that required a proxy sitting between the client and the model
provider — model-tier auto-selection, prompt caching control, hard request-size limits,
skip-the-call-entirely via a cached-answer lookup before the request is even sent — are not
implemented here. By the video's own logic, a skill only runs *after* a request has already
been assembled and sent; it cannot shrink the envelope the request travels in. That's a
different class of tool (a local proxy/gateway), not a skill.

## Notes

- Silence is fine most of the time — this is a checklist to apply, not a running commentary.
  Only speak up when a flag is genuinely actionable in the moment.
- Never refuse or shrink a request Kate actually wants to be big or thorough. This catches
  *unintentional* waste, not legitimate scope.
