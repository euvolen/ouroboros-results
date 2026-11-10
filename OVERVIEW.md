# Ouroboros

Ouroboros is a local inference engine for applications that work with text, images, speech and other model outputs. It gives developers a common interface for requesting work, following its progress and collecting the results on their own hardware.

A workflow can use several kinds of models to produce one deliverable. Our demonstrations include illustrated films with narration and music, science explainers, and comics assembled into PDFs.

## Capabilities demonstrated

- **Multiple model types.** Tested execution paths cover text generation, images, speech synthesis, music, video generation, vision, segmentation and image-to-mesh. Support depends on the model architecture, its required components and the installed runtime.
- **Model management.** Discover or download model files, prepare the required components, test a configuration and record its readiness for use.
- **Application integration.** A local API accepts supported tasks and exposes job progress, status and output artifacts. Applications can build their own workflows around it.
- **Inspection and measurement.** Labs provides model management, execution history, telemetry and a benchmark workbench. These help developers evaluate a configuration against the work their application actually performs.

## Finished examples

On a Windows workstation with an AMD Radeon RX 7900 XT and 20 GiB of VRAM:

| Demonstration | Measured result |
| --- | --- |
| Two-page comic, six panels, story prompt to PDF | **3 min 58 s**, compared with **5 min 05 s** using the matched ComfyUI image workflow |
| Two-minute Mentats film, eighteen illustrations, narration and music | **8 min 45 s**, compared with **24 min 21 s** using our earlier Ouroboros configuration |
| Three short science films, including images, narration, music and assembly | **4 min 23 s total** from prepared scripts |

The comic comparison saved 22.0% of elapsed time. The Mentats comparison saved 64.1%. These measurements cover the complete timed workflows described in the accompanying results.

The science and Mentats films combine generated still images, speech, music, captions and editing. Their production times measure that illustrated-film workflow.

Watch the [finished videos and their timing records](videos/README.md). Read the [comparison conditions and quality findings](README.md).

## Building on the engine

An application submits supported tasks to the local service, follows their progress and uses the returned artifacts in its next step. This supports assistants, media tools and other applications that need several kinds of local inference.

Riddle is one application being built on Ouroboros. Its workflows connect model tasks into larger jobs, such as preparing a story, generating illustrations and reviewing the result.

Ouroboros is under active development. Current evidence covers specific tested models and configurations. The published measurements come from one workstation, with sample counts and timing boundaries stated alongside the results. The examples also retain their quality findings, including comic continuity issues and a Mentats audio mix that needs further work.
