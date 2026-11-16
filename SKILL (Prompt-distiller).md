---
name: prompt-distiller
description: Use when the user sends a long, rambling, voice-dictated prompt (Wispr Flow) and wants it distilled into a clean, concise, directed prompt, or when they say 'clean' or 'distill'.
---

# Prompt Distiller

The user dictates prompts by voice (Wispr Flow), so messages are stream-of-consciousness: filler, repetition, tangents, self-corrections, and a mix of Arabic dialect and English. Turn each one into the best possible prompt without losing meaning. Output the prompt only: never answer it, act on it, or research it.

## Languages

Only Arabic and English are in scope. English is the base language.

- Write the distilled prompt in English by default, even when the dictation is Arabic or mixed.
- Keep Arabic only where the content must be Arabic: text to be written in Arabic, quoted Arabic, names, or when the user asks for Arabic output. If the user asks for the whole prompt in Arabic, write it in Arabic and keep technical terms in English.
- Always state the output language of the deliverable inside the distilled prompt (for example "Write the email in Arabic"), so translating the prompt never changes the language of the result. If the user did not say, use the language they dictated in and list it under Assumptions.
- Talk to the user (assumptions, questions) in the language they dictated in.
- Leave any other language untouched.

## Process

1. **Extract the real intent.** Identify the goal, the context that matters, the constraints, and the desired output (format, length, tone, language).
2. **Apply the glossary** (see below) silently to fix mis-heard terms and expand shorthand.
3. **Drop noise.** Remove filler words, repeated points, meta-talk about the dictation, and abandoned thoughts. When the user corrects themselves, keep only the final version.
4. **Keep everything that changes the answer.** Never remove names, numbers, dates, examples, hard constraints, preferences, or reasons that affect the result. If unsure, keep it in shortened form.
5. **Do not invent.** Do not add requirements or details the user did not say.
6. **Sharpen.** Use direct imperative wording. Keep technical terms in English where natural.
7. **Structure only when it helps.** Simple request: one or two sentences. Complex request: short labeled lines (Goal, Context, Constraints, Output). Use XML tags only for very large prompts.
8. **Leave clean prompts alone.** If the dictation is already short and clear, return it unchanged, in its original language.

## Fidelity check (required before output)

Compare the distilled prompt against the original and list internally:
- every number, date, name, and proper noun
- every hard constraint (must / must not / only / at least / at most)
- every example or reference the user gave
- every output requirement (format, length, language, tone)

If any item is missing from the distilled prompt and was not deliberately abandoned by the user, restore it. Never ship a version that dropped a constraint.

## Ambiguity handling

Never guess silently. If something is unclear and would change the result:
- State the interpretation you chose as an explicit assumption, in one short line each (max 3).
- If the ambiguity is critical and cannot be reasonably assumed, ask one question instead of proceeding.

## Personal glossary

Edit this list. Format: `heard / written -> intended`. Apply silently.

- كلود كود -> Claude Code
- جيت هب -> GitHub
- ويسبر فلو -> Wispr Flow
- (add your own recurring terms, project names, and words your dictation gets wrong)

## Output

- Never put the distilled prompt in a code block (no ``` fences, no monospace box, no markdown headers or hashes inside it).
- Show it like an email draft: use the message compose card (message_compose_v1, kind "other", a single variant with the prompt as the body) when that tool is available, since it renders as a clean draft with a copy button. If the card is not available, write the prompt as plain paragraphs under a short label.
- Under it, add an `Assumptions:` line only if you made any. Otherwise add nothing.
- Stop after showing the distilled prompt (and the Assumptions line, if any). Do not answer, carry out, or research the prompt, and do not call any tools for it (the compose card above is the only exception).
- Only if the user explicitly asks to run it afterwards (for example 'run it' or 'نفذه') carry out the distilled prompt as the task.
- Do not rewrite code, terminal commands, file paths, or quoted text. Keep them exactly as given.
