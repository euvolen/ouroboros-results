# What can an application do with a model’s judgment?

Imagine asking an application to turn a story into a comic. Who decides where the first panel ends? The page editor knows how to place six images. A model can read a new story and decide which six moments to draw. Once that decision comes back as six panel descriptions, software can commission the illustrations, lay out the pages and return a PDF. The author can spend their attention on whether the reader can follow the story.

**This is the idea behind Riddle. A developer can give part of an application a job that requires judgment, then write what happens with the answer.** A *spell* describes who gets which evidence, which tools they can use, what can proceed independently and what must pass a check. Ouroboros supplies local inference. The spell gives those calls a purpose.

On one Windows workstation with an AMD Radeon RX 7900 XT (20 GB), a two-page comic took **3 min 58 s** with Ouroboros and **5 min 05 s** with the matched ComfyUI image workflow. Both clocks started at the story prompt and stopped at the finished PDF.

We have a finished PDF and a timing result. We also found continuity problems. That distinction matters to the person commissioning the comic: the engine can deliver all six panels on time while the story still needs an editor.

## Why orchestrate?

In chat, a person often acts as the application. They read the plan, copy each scene to an image tool, decide what to redo and assemble the result. A spell lets the author describe those handoffs once. Models can interpret each new input or propose a revision. Ordinary code can measure a file, run a test or render the final cut. The person can retain the decisions they actually care about, such as approving the story before illustration begins.

Language makes this a different kind of programming. “Choose the moment when the reader first understands the danger” can be an executable instruction even when nobody can specify a reliable formula for choosing that moment. Tokens represent a model’s input or output, and embeddings encode features numerically. The application can pass a scene list, an image, a test result or a request for human review between steps. What makes those steps useful together is their agreement about what each result means and who may act on it.

| Application | What orchestration makes possible | What we have shown |
| --- | --- | --- |
| A media studio | The author gives story direction. A planner chooses scenes, generators supply assets, and an editor assembles them. A continuity review can send a particular scene back for revision. | Story prompt to comic PDF and prepared scripts to finished films. Continuity and final audio quality still needed review. |
| A development team | Opus could investigate a bug and author a spell that a local worker uses to reproduce and fix it. Sol could independently author a review using the bug report and test evidence. Routine reruns could stay local while a disputed design decision goes back to the planner. | Legacy supports spell authoring, local and cloud model selection, bounded delegation, sandboxed coding tools and saved evaluations. This exact two-author repair and review is a proposed experiment. |
| An assistant away from the desk | A recurring workflow could collect updates locally, compare them with yesterday’s state and notify the user only when a decision is due. The user could inspect the evidence and steer the work from a phone. | Legacy has interval Rituals and run history. The newer assistant separately demonstrated creating a goal, running a local brief and reviewing its cited suggestion from a phone. In one trial, 12 of the first 17 briefs met the usefulness rubric. |
| A robot sharing space with people | While a CPU controller follows a path, an NPU could watch for obstacles and a GPU model could interpret an unfamiliar scene. Each observation needs a timestamp. The controller must be able to stop even if interpretation is late. | We have exercised vision and segmentation on tested inputs. Concurrent perception, movement and reaction on a physical robot remain an experiment. |

One further possibility follows from the development example. **A model can produce a procedure as its deliverable.** A team could inspect that procedure, test it on a known bug, grant it limited tools and reuse it on the next issue. That would let one expensive planning session improve many cheaper local runs. We have yet to measure whether the savings survive the cost of authoring, review and failed runs.

For a first look at the authoring tools, follow a dispatch note from a local answer to a saved check, then inspect a four-step run whose final writer failed. [Illustrated Riddle Legacy walkthrough](riddle-core-legacy/README.md#the-second-time-you-do-the-job).

## Media workflows

Watch the [Mentats films and three science shorts](videos/README.md), with their recorded production times and downloadable MP4s.

Times are elapsed seconds. The last column gives the percentage of baseline time saved.

| Timed work | Baseline | Ouroboros comparison | Time saved |
| --- | --- | --- | ---: |
| Two-page wordless comic, six panels, prompt to PDF | ComfyUI image workflow · 304.82 s | Ouroboros image workflow · 237.90 s | **22.0%** |
| One page of six 512 × 512 panels | Fresh image session per panel · 362.44 s | One session for the page · 89.86 s | **75.2%** |
| Two-minute illustrated film, prepared script to verified MP4 | Separate portrait jobs · 1,461.22 s | Grouped portrait jobs · 525.11 s | **64.1%** |

**Comic.** We changed the image backend in the same research workflow. Both configurations used Z-Image Turbo with matched F16 settings, storyboards, prompts and seeds. We ran each twice, reversing the order for the second pair. The table gives medians. Rendering took 183.93 s with ComfyUI and 112.93 s with Ouroboros. Planning still took about 69 s in both, which explains why the saving on the whole PDF was smaller. Visual review found continuity issues, and human approval was pending.

**Six-panel page.** Both sides used Ouroboros. Keeping the image session available spread its startup cost across six requests. Across two runs per configuration, every decoded panel matched its counterpart and all four PDF pages rendered identically.

**Film.** One run per configuration included 18 portraits, narration, music, editing and verification. Grouping brought the portrait stage from 1,209.56 s to 285.63 s. All 18 portraits matched the baseline. Only one sampler was active at a time in the grouped run. On the final audio mix, a speech recognizer made 42 word edits against the 299-word script on the baseline mix and 131 on the grouped mix. Checking the scenes individually gave 42 and 45 edits, respectively.

## The size of the image job changes the result

On the same 20 GB AMD station, we timed how long a client waited for Z-Image Turbo to deliver one or more views of a red gear. Each cell is one run with the same weights at 512 × 512. Both clients delivered the requested count. Renders differed across engines, so these times establish delivery speed on this fixture only.

| Images requested | Ouroboros installed node | Lemonade v2026.45.3, released backend | Lemonade, matched diffusion binary |
| --- | ---: | ---: | ---: |
| One | 87.01 s | 197.30 s | **69.48 s** |
| Eight | **98.16 s** | 533.41 s | 109.05 s |

For someone waiting for one preview, matched Lemonade finished about 18 seconds sooner. For someone waiting for eight variants, Ouroboros delivered the set about 11 seconds sooner. Changing Lemonade’s backend and compatible settings closed most of the original batch gap. The products used their respective delivery formats, and first-use effects were visible. A separate text → image → text workflow finished in 88.41 s on Ouroboros and 94.37 s on matched Lemonade. Its final check read the image dimensions from a manifest. [Lemonade release used in the comparison](https://github.com/lemonade-sdk/lemonade/releases/tag/v2026.45.3).

## Repeated text work

A reviewer sometimes asks a short follow-up about material it has already read. We timed the same two-step text workflow with its earlier context reset or retained. These were synthetic repeated inputs with eight-token completions. Each timing is a median over six measurements in two sessions. The timer started after model loading.

| Model and approximate shared input | Reset | Retained | Time saved |
| --- | ---: | ---: | ---: |
| Qwythos 9B · 16k tokens | 19.81 s | 10.16 s | **48.7%** |
| Devstral Small 2 24B · 4k tokens | 59.29 s | 35.27 s | **40.5%** |

The output tokens matched between configurations for both models. In a separate Qwythos test with six document-and-question packets, the follow-ups reused zero tokens and showed no demonstrated benefit from retention. The shape of the request matters.

## Where this helps Riddle

A Riddle comic spell could keep the drawing session available until every panel is ready, then hand the page to a reviewer. The prompt-to-PDF test saved **about 67 seconds** on the two-page story. For a narrated-short spell, the difference between the two speech checks makes the final audio mix worth reviewing alongside individual scenes.

Riddle also lets a user create a daily-brief goal on their phone, run it locally, inspect the cited note and accept or decline the suggestion. In a separate trial, 12 of the first 17 briefs met the usefulness rubric. The fifth miss put the target of 36 out of 40 out of reach. The misses included suggestions to start work that was blocked or already finished.

*Measurements from 5–10 November 2026. These are project-run results on one station. The ComfyUI comparison covers the two-page comic. The Lemonade comparison covers the image requests and handoff described above.*

## Riddle Legacy walkthrough

Follow a delivery-planning spell from the visual builder to its execution trace, then see how Workbench evaluates a local model and how the desktop connects to inference providers. [Open the illustrated walkthrough](riddle-core-legacy/README.md).
