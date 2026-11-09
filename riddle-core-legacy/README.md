# Inside Riddle Legacy

Riddle Legacy is a desktop workbench for building and testing AI workflows. A **skill** gives a model one job. A **spell** connects skills and tools into a graph. A **cast** is one execution of that graph, with its own inputs, outputs and history.

We asked the desktop to plan a delivery using four tasks and ten days of capacity. A tool supplied the figures, two model steps examined them, and a final step tried to write the plan. Following that cast from the builder to its result shows where a workflow can succeed mechanically and still disappoint its reader.

### Build the workflow in the Laboratory

Open **Laboratory → Spell builder** and select **Capacity-Checked Delivery Plan**. Read the graph from left to right. **Calculate** runs a tool against the example task data. Its output goes to **scope**, **risk**, and the final **plan** step. The two analysis steps also send their findings to **plan**. Those arrows determine which evidence is available when the writer runs.

Select a step to inspect its instructions, model binding and tool access. Select a connection to inspect how it delivers an output. **Validate** checks the graph before saving. This example had four steps, seven arrows, zero blocking issues and three context warnings.

![Spell Builder showing the calculation, scope and risk branches, and final planning step](images/01-spell-builder.png)

### Cast it and read the Loom

Start the workspace container, choose the saved spell, enter the delivery request and select **Run spell**. Open the completed cast in **The Loom → Run history**. The timeline locates each execution in time. The **Signals** row lists the actual handoffs. Selecting an execution opens its inputs and output.

On this station, the cast completed all four steps in **25.1 seconds**. The calculation supplied nine days of effort and a seven-day critical path. The final model output was a tool-call-shaped fragment where a reader needed a milestone plan. A completed trace answered “Did the steps run?” An evaluation of the deliverable would also need to ask “Did the reader get a usable plan?”

![Loom timeline of the completed four-step delivery cast, including the signals between steps](images/07-loom.png)

### Try one part in Workbench

Open **Laboratory → Workbench → Experiments**. The library lets you choose a skill, a saved step, a group or a whole spell. Start with a small input so you can tell exactly where a mistake enters.

For a second example, we selected **Example Evidence Writer** and supplied a dispatch note. The 10:00 collection had been cancelled and the 14:00 replacement was confirmed by source **KB-17**. The local model returned the new time and the source ID. Workbench retained the result and reported **142 tokens and 2.20 seconds**. Select a run in the left column to revisit its draft and final output.

![Workbench showing a completed local Evidence Writer run and its selected output](images/02-workbench.png)

### Turn the example into a repeatable check

In **Workbench → Spells**, select **Evidence Brief Helper**, then **Evaluations → New case**. Enter the dispatch prompt, choose **Contains every value**, and put `14:00` and `KB-17` on separate lines. Save the case and select **Run case**. The report shows the assertion results and the actors that actually ran.

The one-step spell passed **1/1 cases** on local Qwen2.5-1.5B-Instruct. The check establishes that both expected strings occurred and execution succeeded. It leaves open whether the wording is clear or whether the answer also contains a contradictory time. For the larger delivery spell, a useful case would check the capacity figures, dependencies and presence of an actual milestone plan.

![Workbench Evaluations showing the saved dispatch case, the expected values and the passing result](images/03-evaluations.png)

### Choose where inference runs

Open **Settings → Engines**. The connection you configure here supplies choices to chat and spell model pickers. A step can inherit the run's model or pin a particular one.

| Route | How to set it up | What the choice means |
| --- | --- | --- |
| **Local** | Use the managed llama.cpp engine. **Models** is where you add or download weights. **Runtime** is where you validate, load and unload the selection. | The selected local model runs on the station. This walkthrough used CPU inference. **Settings → ComfyUI** manages the separate media workflow and model setup. |
| **Cloud** | Choose an OpenAI or Anthropic preset, set the endpoint and supply the **name** of the environment variable holding the API key. Discover models, then select one. | Requests use that API connection and its billing. Other compatible endpoints are experimental. |
| **Subscriptions** | Enable a provider card, save the CLI location or use automatic detection, check the existing login and choose an available model. | Riddle uses the installed provider CLI. Cursor, Codex and Antigravity have desktop cards. The provider account determines availability and usage limits. |

**Local engine.** The enabled llama.cpp endpoint discovered the model used for the example runs.

![Local engine settings showing the default llama.cpp endpoint and a discovered model](images/04-local-engine.png)

**Cloud engine.** The OpenAI preset fills in the protocol and API endpoint. The credential field takes an environment-variable name.

![Cloud engine settings with the OpenAI preset values and the API key variable name](images/05-cloud-engines.png)

**Subscription connections.** These experimental cards offer a login check, model selection and a streamed text preview. An explicitly selected subscription stays bound to that connection and model. Unsupported requests fail before inference. The Codex connection can also use explicitly granted Riddle function tools in supported sessions. The screenshots show disconnected accounts. All inference in this walkthrough ran locally.

![Subscription settings showing the Cursor, Codex and Antigravity cards](images/06-subscriptions.png)

*Captured November 9, 2026, using the legacy desktop frontend and desktop API from revision `7217388`, in a browser with disposable example workspaces. Timings are single-run observations. The delivery cast and the dispatch-note evaluation are separate examples. The [Ouroboros benchmark results](../README.md) cover separate engine comparisons.*
