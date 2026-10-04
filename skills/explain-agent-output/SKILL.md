---
name: explain-agent-output
description: Explain complex agent output for human review using clear writing, a diagram, an interactive HTML page, or a video when requested. Use for explanations and walkthroughs, not routine coding status updates.
license: MIT
---

# Explain Agent Output

Inspired by [Karpathy's post on understanding model outputs](https://x.com/karpathy/status/2105819303471976479). As agents do more work, help the person inspect what happened and why. Keep the original artifact available; an explanation is not evidence that the work is correct.

Choose the least elaborate format that makes the important relationships clear. Follow the user's requested format when one is specified.

- **Writing:** Lead with the result, then the reasoning and uncertainties. For dense technical prose, try the clarity of ASD-STE100 (or a relaxed version), but do not claim formal compliance unless checked against the specification.
- **Diagram or image:** Use one when structure, flow, or comparison is easier to understand visually. Label inputs, outputs, and assumptions; include a brief text explanation so the meaning does not depend on the image alone.
- **Interactive HTML:** Use when the reader benefits from exploring states, steps, or alternatives. Make it usable without an account or unnecessary external dependencies, and keep the underlying facts inspectable.
- **Explainer video:** Make one when the user asks for it and the available tools support it. Start with a short script and storyboard, then check narration, visuals, captions, and playback. Do not require ElevenLabs or any particular paid service; ask before using a paid external service or sending sensitive material to one. Never put an API key in the artifact.

Whichever format you choose, separate verified facts from interpretation, cite or link the source work, and test the resulting artifact before handing it over. If a requested format cannot be produced with the available tools, say what is missing and offer a simpler format.
