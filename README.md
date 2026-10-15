# Think Out Loud

**Technical skill name:** `voice-prompt-interpreter`

Think Out Loud helps turn unfinished spoken or typed thinking into a clear, reviewable prompt. It preserves corrections, decisions, constraints, parked ideas, and open questions while removing repetition and verbal self-corrections.

By default, the skill compiles the thought stream for review and waits for clear authorization before doing the underlying task. The deliberate exception is one unambiguous instruction to both compile and execute. A compile request by itself never authorizes execution.

## Setup

This repository contains a folder-based skill package. Its host metadata declares `chatgpt`, `codex`, `api`, and `atlas` targets. That metadata is not a guarantee of identical behavior or a host installation guide.

For **Codex**, place the complete `voice-prompt-interpreter` folder under your skills directory:

- Windows: `%USERPROFILE%\.codex\skills\voice-prompt-interpreter\`
- macOS/Linux: `~/.codex/skills/voice-prompt-interpreter/`

If you download this repository as a ZIP, rename the extracted `think-out-loud-main` folder to `voice-prompt-interpreter`, or copy its contents into a folder with that name.

These paths match the installed package location used to prepare this release. For other declared products, use the host's current skill import or installation process; the repository does not provide an installer for them.

Keep `SKILL.md`, `agents/openai.yaml`, `assets/icon.svg`, and both files in `references/` together. The references describe the expected behavior and state transitions.

## Demo

Say:

> Capture this thought: I need a five-minute launch update for Sales. Scratch that, make it ten minutes. Parking lot: maybe add an animation later. Compile this.

The skill should carry forward the ten-minute limit, keep the animation parked outside the active prompt, and show a compiled prompt for review without executing it. After reviewing it, say “run it” to authorize the reviewed prompt.

## Limitations

- The skill works from text and signals its host provides. It does not control a microphone or voice activity detection (VAD) directly.
- It cannot guarantee that interruptions or pauses will be eliminated or detected. If the host does not provide silence or end-of-thought signals, it relies on the user's words and confirmation.

Behavioral examples are included in [`references/acceptance-tests.md`](references/acceptance-tests.md), and canonical transitions are in [`references/state-machine.md`](references/state-machine.md). They were not run as an automated release test suite.

## Credit

Designed by Brian Skena through a human-led design process developed with ChatGPT. This is an independent project and is not endorsed by OpenAI.

## Feedback

If this is useful, a star or honest feedback is welcome and entirely voluntary.

## License

Released under the [MIT License](LICENSE).
