# Inside Riddle Legacy

[Watch the 91-second presentation](inside-riddle-legacy.mp4?raw=true) · [English captions](captions.srt) · [Full desktop walkthrough](../README.md)

The job was to explain the existing desktop using approved screenshots, then deliver a film someone could watch. A Riddle spell connected source checks, writing, speech, music and assembly. The accepted cast completed in **1 min 56 s** on the local RX 7900 XT workstation.

## The executed workflow

| Step | Input | Delivered result |
| --- | --- | --- |
| Check sources | Walkthrough and approved screenshot digests | Grounding material for eight shots |
| Write | Shot direction and its source passage | Eight passages written by local Qwythos 9B |
| Narrate | Each approved passage | Eight local Piper voice recordings |
| Score | Measured narration and slide durations | A 92-second instrumental from local ACE-Step Turbo |
| Assemble and verify | Pictures, speech, score and captions | A 1080p landscape film with eight chapters and a stereo mix |

The [spell definition](presentation.spell.json) shows the actual five-step graph. The [storyboard](storyboard.json) supplies shot directions, public screenshot references and close-up rectangles. These are application-level examples. Running the definition requires its corresponding application bindings and a configured local runtime.

Storyboard crop coordinates are left, top, right and bottom pixel positions within each source screenshot.

Codex helped author the workflow. All seventeen accepted model calls in the measured production went to local inference. Authoring, earlier editorial revisions and encoder checks fall outside the final-cast timing.

The useful separation is visible: models wrote and performed the material; the workflow carried the dependencies; software assembled and verified the file. The final film plays for **91.292 s** and includes selectable English captions. Each screenshot is shown in context before its close-up.

[Output measurements and hash](cast-receipt.json) · [Why orchestration matters](../../README.md)
