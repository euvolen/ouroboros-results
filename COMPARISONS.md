# Recorded comparisons

These results explain where local execution helped particular workloads. The [executed spell demonstrations](README.md#the-value-of-orchestration) separately show how Riddle connects the work. All measurements below come from one Windows workstation with a Radeon RX 7900 XT and 20 GB VRAM.

## Media workflows

| Timed work | Baseline | Comparison | Time saved |
| --- | ---: | ---: | ---: |
| Two-page wordless comic, six pictures, prompt to PDF | ComfyUI image workflow: 304.82 s | Ouroboros image workflow: 237.90 s | **22.0%** |
| One page of six 512 × 512 panels | Fresh image session per panel: 362.44 s | One session for the page: 89.86 s | **75.2%** |
| Two-minute illustrated film, prepared script to verified MP4 | Separate portrait jobs: 1,461.22 s | Grouped portrait jobs: 525.11 s | **64.1%** |

The comic result is the median of two full workflows per engine, with order reversed for the second pair. Both used Z-Image Turbo with matched F16 settings, storyboards, prompts and seeds. Image rendering took 183.93 s with ComfyUI and 112.93 s with Ouroboros; planning still took about 69 s in both. The comparison exercised host production stages rather than the Riddle desktop. Continuity problems remained and human approval was pending.

The six-panel comparison used Ouroboros on both sides. Across two runs per configuration, decoded panels matched their counterparts and the rendered PDF pages matched. Compatible work shared a drawing session across the page.

The film comparison used one run per configuration. All eighteen portraits matched. Only one image sampler was active at a time in the faster run, so the result does not establish simultaneous GPU sampling. Its final audio mix was worse on the recorded speech check: 131 word edits against the 299-word script, compared with 42 on the earlier mix. Checking scenes individually gave 45 and 42 edits. [Watch both files](videos/README.md).

## Request size changes the image result

Same weights, 512 × 512 output, one measured run per cell:

| Images requested | Ouroboros installed node | Lemonade v2026.45.3 released backend | Lemonade with matched diffusion binary |
| --- | ---: | ---: | ---: |
| One | 87.01 s | 197.30 s | **69.48 s** |
| Eight | **98.16 s** | 533.41 s | 109.05 s |

Matched Lemonade delivered one preview about eighteen seconds sooner; Ouroboros delivered eight variants about eleven seconds sooner. Matching the backend and compatible settings closed most of the original batch gap. First-use effects were visible and delivery formats differed. Rendered images differed across engines, so the table measures delivery rather than pixel equality.

A separate text → image → text workload finished in 88.41 s on Ouroboros and 94.37 s on matched Lemonade. Its final check read image dimensions from a manifest; it was not a visual-quality judgment. [Lemonade release used](https://github.com/lemonade-sdk/lemonade/releases/tag/v2026.45.3).

## Repeated text work

A follow-up can benefit when it reads compatible material already processed in the earlier step. In these synthetic two-step cases, completion length was eight tokens and timing started after loading. Each value is a median over six measurements in two sessions.

| Model and shared input | Reset context | Retained context | Time saved |
| --- | ---: | ---: | ---: |
| Qwythos 9B · about 16k tokens | 19.81 s | 10.16 s | **48.7%** |
| Devstral Small 2 24B · about 4k tokens | 59.29 s | 35.27 s | **40.5%** |

Output tokens matched between configurations. A separate Qwythos case with six document/question packets reused zero tokens and showed no demonstrated retention benefit. These synthetic timings do not establish better answers or the same saving for every request.

## Repeated audio work

Two fixed eight-second ACE-Step Turbo cues used the same model, prompts, seeds and generation settings. Values are medians from two measured runs per configuration after warm-up.

| Configuration | Complete two-cue workflow | Sampled peak dedicated VRAM |
| --- | ---: | ---: |
| Fresh model session for each cue | 9.2720 s | 3.054 GiB |
| Keep one compatible session | **5.4002 s** | 6.425 GiB |

Elapsed time fell **41.76%**, with matching waveforms and greater VRAM use. The clock included startup, both outputs, memory sampling and exit. Existing filesystem and driver caches were retained.

The tested XL model also exposed a limit: one request order increased elapsed time from 14.5278 s to 17.2324 s; reversing the cues changed the result to 14.3567 s versus 10.3637 s. Model and request shape matter. These two-cue measurements are separate from the album's accepted-job timing totals.

## Reading the results

Orchestration makes the application's jobs, dependencies and checks explicit. Compatible execution can reduce repeated work, and these tables measure particular instances of that benefit. Human authoring effort, output quality, cloud cost and physical robot reaction time are separate questions.

[Return to the value and showcases](README.md).

Recorded 5–11 November 2026. Sample counts and timing boundaries vary by case; these are project-run measurements on one workstation.
