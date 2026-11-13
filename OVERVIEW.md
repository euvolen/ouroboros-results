# Ouroboros and Riddle

**The useful result is a finished job someone can inspect and repeat.** Ouroboros provides local inference; Riddle connects model judgment and ordinary software into workflows that deliver that result.

## Two responsibilities

| Part | Responsibility |
| --- | --- |
| Ouroboros | Run supported local model tasks and expose their progress and output artifacts |
| Riddle | Describe the purpose, inputs, handoffs, tools, branches and checks of the application workflow |
| The application or operator | Review the result, decide what is acceptable and act on the evidence |

A spell can combine several model types with deterministic tools. A model can interpret a brief, another can create an image or song, and software can assemble the files or measure a physical outcome. The workflow makes those agreements explicit.

## Demonstrated work

- [An album](albums/neverland-lab-experiments/README.md): writing, artwork, songs, lyrics, story and downloadable player.
- [A presentation](riddle-core-legacy/presentation/README.md): approved screenshots to locally written narration, speech, music and a finished film.
- [A robot task](robotics/robosuite-pick-place/README.md): local-model decisions cooperating with an existing simulated controller, with measured placement and recovery.
- [Authoring and review](riddle-core-legacy/README.md): a visual workflow, retained handoffs, saved checks and visible failures.

The examples substantiate orchestration and integration on their stated cases. They also preserve weak outputs and failed tasks. A graph running to completion does not by itself establish that its final answer is useful.

## Local execution

Tested execution paths include text, images, speech, music, video, vision, segmentation and image-to-mesh. Availability depends on the model architecture, components and runtime. Model management, a local API, job records and Labs supply the engine-facing controls; the assistant and other applications build their own experiences on top.

The [gallery and explanation](README.md) lead with the application value. [Recorded comparisons](COMPARISONS.md) describe particular execution results and their limits. Neither is a claim of universal model compatibility or physical robot safety.
