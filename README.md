# humanize-text-skill

A Claude Code skill that rewrites AI-generated text to sound like a real person wrote it.

## What it does

Takes text that reads like it came out of a language model and rewrites it until an AI detector can't tell the difference. It removes the vocabulary, grammar patterns, and structural tells that make AI writing recognizable, then adds back the rhythm, opinions, and specificity that make writing feel human.

The skill uses a two-pass process: a first rewrite to strip the obvious patterns, then a self-audit pass that asks "what still makes this obviously AI?" and revises based on the answer. The second pass is where most of the remaining detection risk gets caught.

## Results

Tested against an AI detector on three different text types (corporate strategy, academic research, product announcement), starting from 100% AI-generated originals:

| Text type | Before | After |
|-----------|--------|-------|
| Corporate strategy | 100% AI | 11.1% - "Human written" |
| Academic research | 100% AI | 9.9% - "Human written" |
| Product announcement | 100% AI | 8.1% - "Human written" |

## What it fixes

**Vocabulary** - Replaces Tier 1 red flags (delve, leverage, seamless, pivotal, embark, game-changing, unravel, resilient, thrilled, and 25+ more) and watches for Tier 2 clusters (robust, cutting-edge, comprehensive, etc.)

**Grammar patterns** - Copula avoidance ("serves as" / "stands as" should just be "is"), superficial -ing analyses ("highlighting the importance of..."), negative parallelisms, synonym cycling, false ranges

**Structure** - Formulaic section shapes, identical paragraph lengths, inline-header lists, rule-of-three padding, clean wrap-up conclusions that tie everything together too neatly

**Filler** - Significance inflation, promotional language, vague attributions ("experts argue"), generic conclusions ("the future looks bright"), chatbot artifacts ("I hope this helps!")

**Punctuation and style** - Em dashes, overused hyphenated pairs (data-driven, cross-functional, decision-making), mechanical boldface

**Voice** - Adds contractions, sentence rhythm variation, occasional rhetorical questions, opinions where appropriate, specific details over vague abstractions

## Installation

**Option 1 - agentskill.sh (recommended)**

Run this inside Claude Code:

```
/learn @alfonsomorab/humanize-text-skill
```

Or just tell Claude:

```
Install the skill "humanize-text-skill" from https://agentskill.sh/@alfonsomorab/humanize-text-skill
```

**Option 2 - npx**

```bash
npx skills add alfonsomorab/humanize-text-skill
```

**Option 2 - Manual**

Clone this repo and copy the `SKILL.md` into your Claude Code skills directory:

```bash
mkdir -p ~/.claude/skills/humanize-text-skill
cp humanize-text-skill/SKILL.md ~/.claude/skills/humanize-text-skill/SKILL.md
```

**Option 3 - Download release asset**

Download `humanize-text-skill.skill` from the [latest release](https://github.com/alfonsomorab/humanize-text-skill/releases/latest) and place it in `~/.claude/skills/`.

## Usage

Just paste your text and ask Claude to humanize it:

```
Humanize this: [your text]
```

Or:

```
This sounds too AI, can you rewrite it?
```

The skill triggers automatically when you use phrases like "humanize", "make this more human", "sounds like AI", "remove the AI voice", or "rewrite naturally."

## Background

Built using the [Claude Code skill framework](https://claude.ai/code), incorporating patterns from [Wikipedia's Signs of AI Writing guide](https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing) maintained by WikiProject AI Cleanup, plus iterative testing against a live AI detector across multiple text types and lengths.

The core insight from that Wikipedia guide: LLMs use statistical algorithms to guess what comes next, so the result tends toward the most statistically likely output for the widest variety of cases. That's what makes AI writing recognizable -- it's optimized for average, not for specific.
