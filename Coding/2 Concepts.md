## Models, Harnesses, Agents, Environments
![[AI-components.png|Diagram showing the four components - environment, model, agent, and harness]]

## Smart Zone vs. Dumb Zone
![[dumb-zone.png|150,000 tokens as the current dumb zone threshold (gradually gone up from 100k in previous versions of this course)]]

## Statelessness
![[codebase-as-memory-system.png|Mario Zechner quote about codebase as memory system]]

## Hallucinations
![[hallucination-flowchart.png|Mario Zechner quote about codebase as memory system]]
## Effort
- The first point: avoid `max` effort. Max and even `extra high` are extremely wasteful uses of tokens. Model providers include these settings mainly to push their benchmark scores higher by a few percentage points. If they can squeeze out 2% improvement on benchmarks, that might rank them higher than competitors.
- For a model like GPT 5.6, the difference between low, medium, and high can feel like you're using different models entirely. It's a genuinely impactful difference. However, don't over-optimize your setup by constantly tweaking effort levels per task.
- Instead, pick one setting and stick with it. The author uses **Claude Opus 4.8 with medium effort** and doesn't change it task by task. The reasoning is simple: consistency matters more than optimisation.
- Improving the **harness and environment** improves the whole AI coding setup, because you can swap models later without rebuilding your workflow around them.

| Factor | Low Effort | Medium Effort | High Effort | Max Effort |
|---|---|---|---|---|
| **Cost** | Cheapest | Moderate | Higher | Most expensive |
| **Speed** | Fastest | Fast | Slower | Slowest |
| **Quality** | Basic | Good | Better | Marginally better |
| **Dumb zone risk** | Lowest | Low | Higher | Highest |
| **Best for** | Mechanical edits, simple tasks | Everyday work | Genuinely hard problems | Benchmarking only |

The sweet spot for most work is medium effort. It provides a good balance of cost, speed, and quality without burning through your token budget unnecessarily.

## Choosing a model
- I consider the model to be about 50-50 equal with the harness plus environment. In other words, the model is a very consequential part of the whole operation. If you switch out to a crap model, then you are not going to get anywhere.
- **Check the benchmarks** - Look at performance graphs for the models you use on sites like [DeepSWE](https://deepswe.datacurve.ai/). They show token spend ratios and differences between low, medium, and high.
- **On a subscription, ignore API $/task:** care about **how much of your usage allowance a model burns to complete the task**; output tokens help, but providers can weight models differently.
	- Check the provider’s own **usage docs/dashboard** to see how different models count against your allowance.

## Subagents
![[parallel-subagents.png|Visualization showing multiple subagents spawned in parallel]]
![[recursive-subagents.png|Visualization of nested subagents spawning their own subagents]]
- If subagents can spawn their own subagents, they can independently decompose and delegate their work, making them more capable than subagents limited to doing everything themselves.
	- Depending on harness, some only allow one level deep
	- This is where paying attention to your starting context window pays off. If your starting context is really big, then you're going to pay that cost every time you open a sub-agent. Keeping it small means it's more economical and you get more time in the [smart zone](https://www.aihero.dev/ai-coding-dictionary/smart-zone).