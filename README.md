# prompt-distiller

Prompt Distiller is a Claude skill that converts rambling, voice-dictated prompts into clean, concise, directed ones. Built for Wispr Flow dictation users, it removes filler, repetition, and abandoned thoughts while keeping every number, name, and constraint through a mandatory fidelity check. It applies a personal glossary to fix misheard terms, states assumptions openly instead of guessing, and supports Arabic and English, with English as the default language. The repository contains SKILL.md, the skill's instructions; README.md, setup and usage; examples.md, before-and-after cases usable as evals; and LICENSE, the MIT terms allowing anyone to use, modify, and share it freely with attribution.

## Files

| File | What it is |
|------|------------|
| `SKILL.md` | The skill's instructions. Claude reads this file. |
| `README.md` | This page: overview, install, usage. |
| `examples.md` | Before/after cases. Also a test set for the skill. |
| `LICENSE` | MIT License. |

## Install

**Claude Code:** copy `SKILL.md` to `~/.claude/skills/prompt-distiller/SKILL.md`.

**Claude app:** put `SKILL.md` in a folder named `prompt-distiller`, zip the folder, and upload it where your app accepts custom skills.

## Usage

Send a messy dictated prompt, or say "clean" or "distill". The assistant shows the cleaned prompt in a draft card when available, or as plain paragraphs, followed by any assumptions. It stops without executing the prompt. To execute it, explicitly ask "run it" or "نفذه" afterwards.

## Languages

Arabic and English only. English is the base: the distilled prompt is written in English unless you ask for Arabic or the result itself must be in Arabic. Already clear prompts remain unchanged in their original language.

## Customize

Add your own recurring terms to the glossary section in `SKILL.md`.

## Test it

Run the inputs in `examples.md` after every edit and compare the results with the expected outputs.

## License

MIT. See `LICENSE`.
