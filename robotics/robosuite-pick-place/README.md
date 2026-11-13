# A local model directing a simulated robot

A stock simulated Panda picks up a can, places it in its marked compartment and recovers after a missed grasp or slip. Local-model decisions completed **20/20 ordinary placements and 20/20 recoveries**. A scripted reference passed the same cases too.

[![A simulated Panda completing a placement](assets/poster.jpg)](assets/replay.mp4?raw=true)

[Watch the narrated replay — 59.83 seconds](assets/replay.mp4?raw=true). Playback accelerates movement and omits inference waits.

## Where the model's judgment fits

The executed spell reads the measured state, asks a local model for a bounded task action, sends the action to robosuite's existing controller, then checks what physically happened. Placement follows a measured grasp. A failed grasp can produce a new observation and a bounded recovery attempt.

The application carries those handoffs and keeps the evidence for an operator. The local model chooses task actions; the stock numerical controller moves the robot. A generated request to place the can is different from a verified placement.

Across the scored model runs, **100 local model calls loaded text weights twice and reused them 98 times**. Median client-call time was **2.20 s**, including the two loading calls in that sample. This is a model-call measurement, not a robot reaction or stopping latency.

| Task | Scripted reference | Local-model decisions |
| --- | ---: | ---: |
| Ordinary pick-and-place | 20/20 | 20/20 |
| Placement after a missed grasp or slip | 20/20 | 20/20 |

There were forty distinct held-out scenes, each tested under both configurations: eighty episodes in total. Every recovery episode recorded an unsuccessful first attempt before completing placement.

| Twenty-episode cohort | Scripted reference | Local-model decisions |
| --- | ---: | ---: |
| Ordinary placement, elapsed total | 75.80 s | 173.42 s |
| Recovery, elapsed total | 125.70 s | 287.89 s |

These clocks cover the episode loop and exclude setup and replay production. Simulation was unpaced and paused for model decisions; the numbers are not robot reaction latencies. The scripted reference was faster on this fixed task, so this result demonstrates integration rather than a speed or model-quality advantage.

The decision model was Devstral Small 2 24B Instruct Q4_K_M on a Windows / RX 7900 XT workstation. The scene used robosuite 1.5.2 and MuJoCo 3.3.7. Observations were structured simulator state. Physical hardware and camera-only grasping remain unproven.

[Case outcomes](cases.csv) · [Measurements](results.json) · [File checksums](SHA256SUMS.txt) · [All showcases](../../README.md)
