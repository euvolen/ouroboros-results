# Ouroboros benchmark results

Ouroboros is a local inference engine. Riddle is an assistant built on it. A Riddle workflow, called a *spell*, can use one model to plan a comic, another to draw the panels, and a vision model to check them. The benchmark that matters to the reader is how long they wait for the PDF.

On one Windows workstation with an AMD Radeon RX 7900 XT (20 GB), a two-page comic took **3 min 58 s** with Ouroboros and **5 min 05 s** with the matched ComfyUI image workflow. Both clocks started at the story prompt and stopped at the finished PDF.

**Why would someone move a task out of chat?** Imagine handing tomorrow’s dispatch brief to a colleague. Today you know which note cancelled the morning collection, which source confirmed the replacement, and what to check before sending. A chat can give you today’s answer. With Riddle you can also hand over the instructions and the check. The colleague can run them on a new note and inspect what happened. [See the actual brief and its saved check in Riddle Legacy](riddle-core-legacy/README.md#the-second-time-you-do-the-job).

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
