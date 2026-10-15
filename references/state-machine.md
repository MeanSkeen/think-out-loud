# State Machine Reference

## States

### CAPTURE
Default state after explicit invocation for a voice dump/brainstorm.

Allowed outputs: concise acknowledgement, clarification only when materially necessary, compile proposal after a genuine closure signal.

Forbidden: executing the underlying task solely because enough detail exists.

Transitions:
- explicit compile instruction -> REVIEW
- closure/pause signal -> ask whether to compile; confirmation -> REVIEW; continue -> CAPTURE
- explicit combined compile+execute -> EXECUTE after compilation if unambiguous

### REVIEW
The compiled prompt is visible and execution remains unauthorized.

Transitions:
- revision -> REVIEW with updated prompt
- resumed brainstorming / "go back" -> CAPTURE
- clear execute instruction referring to reviewed prompt -> EXECUTE

### EXECUTE
Use the reviewed prompt as operative task instructions, subject to higher-priority rules and available capabilities.

## Conflict precedence

For conflicting captured propositions, prefer in this order:
1. explicit later decision or replacement;
2. explicit later constraint;
3. explicit earlier decision not revoked;
4. latest active proposition;
5. leave unresolved if the conflict is genuinely ambiguous.

Never let a parked or superseded proposition override an active one.

## Scope of control primitives

A primitive applies to the nearest semantically relevant proposition, not blindly to the previous sentence token. Use discourse meaning.

Example:
"The deck should be 20 minutes. Actually the audience is Sales. Scratch that, ten minutes max."
Interpret the correction as duration 20 -> 10, not as retracting the audience.

## Combined authorization

Examples that may compile and execute in one move:
- "Compile this and then run it."
- "Turn all of that into the prompt and execute it."

Examples that compile only:
- "Turn that into a prompt."
- "Okay, synthesize this."

Examples that execute only from REVIEW:
- "Run it."
- "Proceed."

During CAPTURE, a bare "run it" is ambiguous if there is not yet a reviewed prompt. Ask whether the user wants compilation plus execution rather than silently skipping the review gate.

## Host capability boundary

The skill can reason over signals the host provides. It cannot manufacture access to audio timing, silence duration, microphone state, or end-of-utterance events. If those signals are unavailable, rely on language and explicit user confirmation.
