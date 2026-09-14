---
layout: post
title: "Is Physics Dead?"
subtitle: "Broken benchmarks, and re-evaluating the capabilities of frontier models in physics"
author: "John Sous"
date: 2026-09-14 12:00:00 -0400
description: "An expert audit of physics benchmarks."
permalink: /blogs/is-physics-dead/
---
*Based on [How Good Are Frontier Models at Physics? Expert Re-Grading Reveals Broken Evaluations and Near-Saturation of Leading Benchmarks](https://arxiv.org/abs/2609.13009), arXiv:2609.13009. Thanks to my co-authors Ali Ansari, Haoran Sun, Andy Zeyi Liu, Mark Jabbour, Lucas Baker, and Arman Cohan, and to the Yale physics faculty and graduate researchers who carried out the audits.*

> *Physics is dead.*
> (not Friedrich Nietzche)

AI has already come for mathematics. What of physics?

Anyone who has spent time working with frontier AI models knows that they are capable of astonishing feats of reason, but also of equally shocking mistakes and naïveté. Within the context a research project they still drift, make inconsistent choices, forget previously establish work, and often struggle to identify the next meaningful step despite know the mechanics. To spend a week applying an agent to a difficult problem is to experience both sides of this duality: the somewhat terrifying breadth of its knowledge, and its seemingly inability to put the knowledge to practical use.

In the wake of Navier-Stokes, any question of capability on the mathematics front seems settled. Physics, however, seems to offer some additional barriers that favor humans, such as fuzzier notations of proof and more interactions with the real world. Most concretely, the benchmarks would suggest that frontier AI has yet to approach even graduate level, so physics should be safe for a while.

Is it?

## Looking at the benchmarks


Judging from the leaderboards on popular sites such as Artificial Analysis, physics appears to be one of the last holdouts against the inexorable march of AI capabilities. On CritPt, a benchmark of research-level challenges, GPT-5.6-Sol scored 32% (the latest release, GPT-6 Astra, does no better). On the physics portion of Humanity's Last Exam, it scored 47%. Apparently, even a model good enough to be declared artificial general intelligence gets roughly half of graduate-level physics wrong.

On the surface, this kind of result is plausible even if the latest models are strong enough to answer essentially any analytical question. Physics is not primarily about executing calculations. Mostly, the hardest part is to decide which calculations matter and which form of the question makes sense to tackle. 

According to an old joke, if you hire a physicist to help a dairy farm, they will start by telling you to "assume spherical cow." The joke captures the deeper truth that physicists are concerned mostly with finding the idealization that discards almost everything about a problem while preserving exactly what matters. For example, in 1983, Robert Laughlin set out to explain the fractional quantum Hall effect. The direct approach would have required an approach for a vast number of strongly interacting electrons, beyond any computer. Instead, Laughlin guessed a many-electron wavefunction with the right symmetry and limiting behavior. His guess was correct, and for it he received the Nobel Prize. Another great example is how Kenneth Wilson and Michael Fisher (who were also awarded the Nobel Prize) implemented a brilliant idea for studying phase transitions, where they treated a problem in three spatial dimensions through an expansion around four dimensions, solved it in 4 − ε dimensions, and then set ε = 1. These are not just calculations. They may omit a certain form of rigor, nonetheless they have the quality of being determined by an intuition about which calculation might expose the underlying physics.

After all, perhaps the low leaderboard scores meant that physics remained beyond the reach of the best models. Perhaps we are safe?

## Measuring carefully

We started by trying to understand where the models failed, to analyze the gaps in their reasoning. We collected rejected answers, then handed them to physicists (my amazing students) and asked them to check the grading. 

We were surprised by what we found!

<figure>
  <img src="/assets/benchmark_accuracy.png" alt="Pre-audit and corrected accuracy on six physics benchmarks" style="max-width: 100%; height: auto; display: block; margin: 0 auto;">
  <figcaption style="font-size: 0.9em; color: #666; text-align: center;">Light bars are pre-audit scores, solid bars are scores after correction.</figcaption>
</figure>

First, the evaluation pipeline was rejecting correct answers written in equivalent forms. Second, many benchmark items were defective. We found incorrect arithmetic in reference answers, questions that omitted information needed to choose among the answers, and physics problems whose solutions depend on unstated conventions. Perhaps most surprising, these issues were common even in expert-curated benchmarks, including those featured on Artificial Analysis such as the physics component of Humanity's Last Exam (HLE) and CritPt.[^1]

So we decided to scale up. We worked with faculty members and their students at Yale (and a few external physicists), assigning every individual one or more questions in their field, and implemented a rigorous audit process. We audited the questions and repaired problems whenever a repair was possible. 30 of 50 CMT-Benchmark questions had a defect, as did 21 of the 56 CritPt questions we audited. After correcting graders and repairing or excluding flawed questions, the measured results changed sharply:

| Benchmark | Pre-audit mean@4 | Corrected mean@4 | Corrected pass@4 |
| --- | ---: | ---: | ---: |
| HLE-Physics | 47.3% | 78.7% | 91.4% |
| CMT-Benchmark | 61.0% | 87.2% | 98.0% |
| CritPt | 32.3%* | 87.5% | 94.4% |

*The pre-audit CritPt score is Artificial Analysis's reported mean@5 on 70 challenges. For the corrected results we use the 54 retained challenges.*

There are important qualifications. The corrected scores are computed on retained or repaired question sets, so the pre-audit and corrected values do not always use identical questions. For HLE, we audited only questions rejected for GPT-5.6-Sol. Some runs used tools while others did not. Even the best corrected evaluator we tested still had an error rate of about 4%. These details matter, but none changes the central result, that the original scores substantially understated model performance.

It seems that AI is killing physics. Frontier models now solve nearly all well-posed, closed-ended physics problems in these benchmarks, from undergraduate mechanics to advanced-level condensed matter and field theory. The leaderboards suggest otherwise because they are broken.

## Solving problem-set problems is not doing physics

We have also deployed GPT-based agentic systems we built, on several open problems in theoretical physics. We have not been able to fully solve one. The agents made considerably less progress than comparable systems have made on open mathematics problems, though they produced interesting traces. This shows that physics research may still be beyond the reach of current models.

Put differently, these systems are excellent at portions of an open problem that resemble a problem set. With a concrete question, they can set up and execute the calculation, run numerics, and check limits. What they do not do well yet is *identify* the right calculation at least over several turns that mimic the research workflow.[^2]

## What comes next

**Harder tasks, defined by the community.** The next generation of evaluations should include tasks that are hard in the way physics is hard, where identifying the idealization is part of the problem and there may be no single reference answer. 

**Open challenges.** To learn whether models can do physics rather than physics homework, we should give them open problems and document the attempts publicly, with physicists in the loop. 

**Better agents and harnesses for physics.** Physics needs harnesses that simulate the questions a good researcher would ask in pursuit of an answer to a research problem. The best first targets may be genuinely unsolved problems that are yet within the reach of physicists.

## Is physics dead?

No. The audit suggests that physics benchmarks are saturated. The leaderboard scores do not match what frontier models are able to do. One may feel that if physics benchmarks are saturated, and hard math problems are getting solved almost daily, then it is likely that all closed-ended benchmarks are saturated, and that we need new methods for evaluating AI capability (which on tasks like these is arguably now beyond human ability). What remains beyond reach is the research process.

[^1]: We found some or all of these issues in several benchmarks presented in the paper, and also in our own PHYSICS benchmark, which was not included in the first version of the paper because we did not have time to audit it fully. It will be scrutinized in a future revision.

[^2]: I believe that in response to a single well-crafted prompt, AI finds genuinely creative ideas.
