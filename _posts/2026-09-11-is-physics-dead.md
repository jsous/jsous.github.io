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
> (not Friedrich Nietzsche)

AI has already come for mathematics. What of physics?

Anyone who has spent time working with frontier AI models knows that they are capable of astonishing feats of reason, but also of equally shocking mistakes and naïveté. Within the context of a research project they still drift, make inconsistent choices, forget previously established work, and often struggle to identify the next meaningful step despite knowing the mechanics. To spend a week applying an agent to a difficult problem is to experience both sides of this duality: the somewhat terrifying breadth of its knowledge, and its seeming inability to put the knowledge to practical use.

In the wake of Navier-Stokes, any question of capability on the mathematics front seems settled. Physics, however, seems to offer some additional barriers that favor humans, such as fuzzier notions of proof and more interactions with the real world. Most concretely, the benchmarks would suggest that frontier AI has yet to approach even graduate level, so physics should be safe for a while.

Is it?

## Looking at the benchmarks


Judging from the leaderboards on popular sites such as Artificial Analysis, physics appears to be one of the last holdouts against the inexorable march of AI capabilities. On CritPt, a benchmark of research-level challenges, GPT-5.6 Sol scored 32% (the latest release, GPT-6 Astra, does no better). On the physics portion of Humanity's Last Exam, it scored 47%. Apparently, even a model good enough to be declared artificial general intelligence gets roughly half of graduate-level physics wrong.

On the surface, this kind of result is plausible even if the latest models are strong enough to answer essentially any analytical question. Physics is not primarily about executing calculations. Mostly, the hardest part is to decide which calculations matter and which form of the question makes sense to tackle. 

According to an old joke, if you hire a physicist to help a dairy farm, they will start by telling you to "assume a spherical cow." The joke captures the deeper truth that physicists are concerned mostly with finding the idealization that discards almost everything about a problem while preserving exactly what matters. For example, in 1983, Robert Laughlin set out to explain the fractional quantum Hall effect. The direct approach would have required an approach for a vast number of strongly interacting electrons, beyond any computer. Instead, Laughlin guessed a many-electron wavefunction with the right symmetry and limiting behavior. His guess was correct, and for it he received the Nobel Prize. Another great example is how Kenneth Wilson (who was also awarded the Nobel Prize) and Michael Fisher implemented a brilliant idea for studying phase transitions, where they treated a problem in three spatial dimensions through an expansion around four dimensions, solved it in 4 − ε dimensions, and then set ε = 1. These are not just calculations. They may omit a certain form of rigor, nonetheless they have the quality of being determined by an intuition about which calculation might expose the underlying physics.

After all, perhaps the low leaderboard scores meant that physics remained beyond the reach of the best models. Perhaps we are safe?

## Measuring carefully

In an effort to explain the gap between frontier model performance on physics and mathematics benchmarks, we looked at why the models failed. Unlike most benchmark analyses, which seek to understand gaps in AI ability at scale and parse differences in statistics, we decided it was necessary to interrogate the questions in detail. We collected questions where the AI answers had largely been rejected, handed them to highly qualified physicists (my amazing students!), and asked them to check the grading.

To put it lightly, we were surprised.

<figure>
  <img src="/assets/benchmark_accuracy.png" alt="Pre-audit and corrected accuracy on six physics benchmarks" style="max-width: 100%; height: auto; display: block; margin: 0 auto;">
  <figcaption style="font-size: 0.9em; color: #666; text-align: center;">Light bars are pre-audit scores, solid bars are scores after correction.</figcaption>
</figure>

Across all benchmarks, we found that a large majority of questions where frontier model answers were rejected were false negatives, either because the evaluation pipeline rejected equivalent forms of correct answers or because the benchmark items themselves were defective. We found incorrect arithmetic in reference answers, omissions of key information leading to underspecified problem statements, and problems whose results depended on unstated conventions. Most surprisingly, these issues were also prevalent in the expert-curated benchmarks used to evaluate frontier physics capabilities, including CritPt and the physics component of Humanity's Last Exam. [^1]

We worked with faculty members and their students at Yale (and a few external physicists) to scale the audit process, assigning every individual question in their area of expertise and attempting repairs wherever possible. We found defects in 30 of 50 CMT-Benchmark questions and 21 of 56 CritPt questions. After correcting graders and repairing or excluding flawed questions, we found that not only were the results enormously different pre- and post-audit, but the strongest models available at the time of audit approached saturation on even the hardest benchmarks. 

| Benchmark | Pre-audit mean@4 | Corrected mean@4 | Corrected pass@4 |
| --- | ---: | ---: | ---: |
| HLE-Physics | 47.3% | 78.7% | 91.4% |
| CMT-Benchmark | 61.0% | 87.2% | 98.0% |
| CritPt | 32.3%* | 87.5% | 94.4% |

*The pre-audit CritPt figure is reported mean@5 on all 70 challenges according to Artificial Analysis. Our corrected results use the 54 retained challenges.*

There are important qualifications: corrected scores are computed on retained or repaired questions, some runs used tools while others did not, and our HLE audit only covered questions where GPT-5.6 Sol’s answers had been initially rejected. In addition, even the corrected evaluator had an error rate of about 4%. However, none of these factors affect the central conclusion that all physics benchmarks have been dramatically understating frontier AI capabilities in physics and continue to do so.

To restate: even the prior generation of frontier models (Fable 5 and GPT-5.6 Sol) now solve nearly all well-posed, closed-form physics problems in every available benchmark, from undergraduate mechanics to research-level condensed matter theory. The belief that benchmarks imply some key difference between physics and mathematics, programming, and other areas where AI capabilities now approach superhuman levels is no more than a comforting fiction.

None of this implies that physics is dead, that agents will replace human physicists, or even that everything important about physics can be reduced to a form that is cleanly solvable by AI. However, it strongly suggests a rude surprise awaits anyone who believes the progression that has so far advanced through chess, Go, poker, protein folding, programming, and now mathematics is about to stop at physics.

## Physics is not yet solved

Given the evidence that physics and mathematics are trending strongly in the same direction, we were also curious whether they would make similar progress on open questions. Our results in this area, although not reported in the paper, look a bit more optimistic for the physicists.

We tested a GPT-based agentic system, which previously succeeded in resolving several open mathematical conjectures, on open problems in theoretical physics. To our temporary relief and encouragement, it has not managed to fully resolve even one autonomously. We also noted that these agents made considerably less progress on the partially resolved physics problems than on open mathematics problems of comparable difficulty, both by our analysis and independent agent-based analysis of partial results in each domain.

Our preliminary conclusion is that the difference comes down exactly to the gaps in high-level intuition that one notices working with these systems in person, and that these gaps may prove more of an obstacle to physics research than to mathematics because problem formulation is a more critical component of what makes a physics question “open”. In other words, frontier models are demonstrably excellent at the portions of any research problem that resemble a problem set. Calculations, numerics, limit-checking, and efficient program formulation are no problem: what they lack is the meta-awareness to step back and ask not only what can be solved but what should be. So far, the traces demonstrate ample evidence of understanding the problem as posed, but not the fundamental will to reshape the question that made approaches such as Laughlin’s, Wilson’s, and Fisher’s possible. 

## Redefining frontier physics for AI

Given that all existing benchmarks are approaching saturation, what do we need in order to get a true picture of AI capabilities in physics research?

**Harder tasks.** The next generation of benchmarks should focus on tasks that emphasize the unique difficulties of physics, favoring those where choosing a favorable representation is part of the problem and there may not be a single reference answer. This will also require a more careful effort to create standards of evaluation flexible enough to admit any answer a qualified physicist would deem correct without relying purely on agentic self-judgment.

**Better agents and harnesses for physics.** AI physics currently lacks the infrastructure of AI mathematics. Besides the simple fact that far more effort has been devoted to the latter, the prominence of Lean has contributed critically to the progression of AI mathematical capabilities. So far, physics has no clear parallel. We need verification tools built around our own culture: limiting cases, dimensional analysis, agreement with known results, and simply better ways of asking the questions that used to exist only on a blackboard. Before tackling the most famous grand challenges, we can develop these tools to address open problems with a more well-defined space of plausible idealizations.

**Open challenges.** We must establish a process of cooperation between humans and AI on open physics questions, including publicly documenting attempts, analyzing partial progress and instructive failures, and creating models for interpretable AI-driven physics research that contributes to human knowledge. Mathematics, as stated by Toffoli and Duede, is not merely the production of solutions, and nor is physics. Results should be comprehensible to humans, and we should have a definite idea of what positive collaboration looks like.

It is always tempting to stick our heads in the sand. What makes this moment unique for physicists is that it is equally easy to do so in several ways: naïve faith in the benchmark gaps, an emphasis on the intuition and judgment supposedly unique to humans, or a refusal to furnish the tools that have helped power the recent progress of AI in mathematics. We propose that the braver and more tenable choice is to face facts directly and help steer the evolution of cooperation between humans and AI. What would it look like to have a process where both sides contribute, results are pursued not for bragging rights or benchmarks but for the evolution of knowledge, and accessibility to human minds remains a core tenet and design component of the research process?

That part is still up to us. 

[^1]: We found some or all of these issues in several benchmarks presented in the paper, and also in our own PHYSICS benchmark, which was not included in the first version of the paper because we did not have time to audit it fully. It will be scrutinized in a future revision.
