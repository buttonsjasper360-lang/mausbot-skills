---
name: expand-and-contract
description: Scope a vague feature request into Core, Nice-to-have, Maybe-later, and Out before delegating it — use when Kate hands you a half-formed idea rather than a concrete task.
---

# Expand and contract

Use this before delegating a task to Cliff or Qwen, whenever Kate's request is a seed idea
rather than a fully-specified task — "make a dashboard for X," "it'd be nice if the bot could
Y," anything where the boundaries aren't stated. Don't run this on requests that are already
concrete and scoped; it adds nothing there.

## The method

**1. Expand first.** Before narrowing anything, list out everything the idea COULD plausibly
include — every adjacent feature, edge case, and nice-to-have someone might reasonably read
into the request. Be generous here; the point is to see the full shape of the idea before
cutting anything, not to guess the minimum.

**2. Sort every item into one of four buckets:**
- **Core** — the request doesn't make sense without this. If you removed it, Kate wouldn't
  recognize the result as what she asked for.
- **Nice-to-have** — clearly improves it, doesn't block shipping without it.
- **Maybe-later** — plausible future direction, not this pass.
- **Out** — related but not actually part of this ask; scope creep if included.

**3. Present the buckets, not just a task list.** When you hand this to Cliff or Qwen (or
summarize it back to Kate for confirmation), show the Core items as what's actually being
built, and name the Nice-to-have/Maybe-later/Out items explicitly rather than silently
dropping them — so a boundary decision is visible and can be corrected before work starts, not
discovered after.

## Why

A delegated task with fuzzy scope either grows in the doing (Cliff or Qwen guessing at what
counts as "done") or under-delivers because a Core piece got missed. Naming the boundary
up front, before assigning anything, is cheaper than re-scoping after code exists.
