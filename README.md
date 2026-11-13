# Ouroboros showcases

Finished local-AI media and robotics demonstrations. Each showcase includes downloadable outputs, recorded results and practical limits. The robot pages distinguish local-model decisions from deterministic movement clips.

| Showcase | Watch or listen | Recorded result |
| --- | --- | --- |
| Illustrated films | [Mentats and three science explainers](videos/README.md) | Two-minute Mentats film: **8 min 45 s**; earlier version: **24 min 21 s**. Three science films: **4 min 23 s together**. |
| Riddle Team music album | [Twelve songs, cover, lyrics and fictional band story](albums/neverland-lab-experiments/README.md) | **24 minutes of music**. Accepted music jobs reported **95.05 s combined**; this excludes the rest of production. |
| A local model directing a simulated robot | [Panda pick-and-place replay](robotics/robosuite-pick-place/README.md) | **20/20 ordinary placements and 20/20 recoveries**. The scripted reference also passed and was faster. |
| Supported humanoid movements | [Wave, thumbs-up and foot movement clips](robotics/humanoid-movement/README.md) | **31 movement profiles** passed in the sampled supported postures. |
| Pause, resume and cancel a wave | [Two recorded lifecycle cases](robotics/wave-lifecycle/README.md) | **20/20 cases:** fourteen completed waves and six cancellations with return. |
| A limit: clapping | [The rejected clap and return](robotics/clap-admission/README.md) | **0/3 claps completed**; all three attempts returned to neutral. |
| Riddle Legacy desktop | [Narrated presentation and screenshot tour](riddle-core-legacy/README.md) | **91-second presentation**, produced locally in **1 min 56 s**. |

## Preview

[![Riddle Team album cover](albums/neverland-lab-experiments/cover.jpg)](albums/neverland-lab-experiments/README.md)

[![A simulated Panda completing a placement](robotics/robosuite-pick-place/assets/poster.jpg)](robotics/robosuite-pick-place/README.md)

Media generation was measured on a Windows workstation with an AMD Radeon RX 7900 XT and 20 GB VRAM. Robot scenes are simulations; their recordings may omit waits or use simulation playback time. Each page states the relevant timing scope.

These examples include failures and quality limitations. They do not establish support for every model, physical robot safety or performance on every GPU.
