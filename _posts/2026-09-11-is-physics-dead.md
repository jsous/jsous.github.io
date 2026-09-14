---
layout: post
title: "Is Physics Dead?"
subtitle: "Broken benchmarks, and what frontier models can and cannot do in physics"
author: "John Sous"
date: 2026-09-11 12:00:00 -0400
description: "What an expert audit of physics benchmarks reveals about frontier models, evaluation, and the parts of physics that remain difficult."
permalink: /blogs/is-physics-dead/
---

> *Physics is dead. Physics remains dead. And we have killed it.*

Is it?

Anyone who works with frontier models knows two things are true at the same time. They can do astonishing things, and they drift. Over a long session they can lose the thread, forget what they have established, and struggle to identify the next useful step in a research project. Both things are true, and anyone who has spent a week with an agent on a hard problem has felt both.

So what about physics?

## The benchmarks said we were safe

If you looked at the leaderboards, physics appeared to be one of the last holdouts. On CritPt, a benchmark of research-level physics challenges, GPT-5.6-Sol scored 32%. On the physics portion of Humanity's Last Exam, it scored 47%. The apparent message was that frontier models still got roughly half of graduate-level physics wrong.

It was tempting to believe that result. Most of the time, the hardest part of physics is not completing a calculation. It is deciding which calculation to do.

There is an old joke about a physicist hired to help a dairy farm who begins with "assume a spherical cow." The joke is on us, but it also captures the craft: physics is the art of finding the idealization that discards almost everything about a problem while preserving exactly what matters. For example, in 1983, Robert Laughlin wanted to explain the fractional quantum Hall effect. The direct approach would have required solving the Schrödinger equation for a vast number of strongly interacting electrons, which is undoable. Instead, Laughlin guessed a many-electron wavefunction with the right symmetry and limiting behavior. His guess was correct, and for it he received the Nobel Prize. Another great example is how Kenneth Wilson and Michael Fisher implemented a brilliant idea for studying phase transitions, where they treated a problem in three spatial dimensions through an expansion around four dimensions, solved it in 4 − ε dimensions, and then set ε = 1. These are not just calculations. They may omit a certain form of rigor, nonetheless they have the quality of being determined by an intuition about which calculation might expose the underlying physics.

After all, perhaps the low leaderboard scores meant that even then, physics remained beyond the models.

## What actually happened

We started by trying to understand where the models failed. We collected rejected answers, then handed them to physicists (my amazing students) and asked them to check the grading. 

We were surprised!

<figure>
  <img src="/assets/benchmark_accuracy.png" alt="Pre-audit and corrected accuracy on six physics benchmarks" style="max-width: 100%; height: auto; display: block; margin: 0 auto;">
  <figcaption style="font-size: 0.9em; color: #666; text-align: center;">Light bars are pre-audit scores, solid bars are scores after correction.</figcaption>
</figure>

First, the evaluation pipeline was rejecting correct answers written in equivalent forms. Second, many benchmark items were defective. We found incorrect arithmetic in reference answers, questions that omitted information needed to choose among the answers, and physics problems whose results depended on unstated conventions. Perhaps most surprising, these issues were common even in expert-curated benchmarks, including those featured on Artificial Analysis such as the physics component of Humanity's Last Exam (HLE) and CritPt.[^1]

So we decided to scale up. We worked with faculty members and their students at Yale, assigning every individual one or more questions in their field, and implemented a rigorous audit process. We audited the questions and repaired problems whenever a repair was possible. Thirty of 50 CMT-Benchmark questions had a defect, as did 21 of the 56 CritPt questions we audited. After correcting graders and repairing or excluding flawed questions, the measured results changed sharply:

| Benchmark | Pre-audit mean@4 | Corrected mean@4 | Corrected pass@4 |
| --- | ---: | ---: | ---: |
| HLE-Physics | 47.3% | 78.7% | 91.4% |
| CMT-Benchmark | 61.0% | 87.2% | 98.0% |
| CritPt | 32.3%* | 87.5% | 94.4% |

*The pre-audit CritPt figure is Artificial Analysis's reported mean@5 on 70 challenges. The corrected results use the 54 retained challenges.*

There are important qualifications. The corrected scores are computed on retained or repaired question sets, so the pre-audit and corrected values do not always use identical questions. For HLE, we audited only questions rejected for GPT-5.6-Sol. Some runs used tools while others did not. Even the best corrected evaluator we tested still had an error rate of about 4%. These details matter, but none changes the central result: the original scores substantially understated model performance.

With apologies to my fellow physicists, AI is killing physics, at least the kind that fits in a problem set. Frontier models now solve nearly all well-posed, closed-ended physics problems in these benchmarks, from undergraduate mechanics to research-adjacent condensed matter theory. The leaderboards suggest otherwise because the leaderboards are broken.

## Does this mean physics is dead?

No. But it tells us that physics is probably next after math on the "chopping block." 

## Solving problems is not doing physics

Alongside the audit, we pointed GPT-based agentic systems we built at several open problems in theoretical physics. We have not been able to fully solve one. The agents made considerably less progress than comparable systems have made on open mathematics problems, though they produced interesting traces.

These systems are excellent at portions of an open problem that resemble a problem set. Give them a concrete question, and they can set up and execute the calculation, run numerics, and check limits. What they do not do well yet is explore the right calculation at least over several turns that mimic the research workflow.[^2]

## What comes next

**Harder tasks, defined by the community.** The next generation of evaluations should include tasks that are hard in the way physics is hard, where choosing the idealization is part of the problem and there may be no single reference answer. Building them will require expert curation, clear conventions, and serious verification.

**Open challenges.** To learn whether models can do physics rather than physics homework, we should give them open problems and document the attempts publicly, with physicists in the loop. Partial progress and instructive failure should both count as useful outcomes.

**Better agents and harnesses for physics.** Physics needs verification tools built around its own culture: limiting cases, dimensional analysis, agreement with known results, numerical sanity checks, and the questions a good researcher asks at a blackboard. The best first targets may not be famous grand challenges, but problems that are genuinely unsolved but with a limited space of plausible idealizations.

## What died, and what did not
The audit suggests that these benchmarks are dead. The leaderboard scores do not match what frontier models are able to do. One may feel that if physics benchmarks are saturated, and hard math problems are getting solved almost daily, then it is likely that all closed-ended benchmarks are saturated, and that we need new methods for evaluating AI capability (which on tasks like these is arguably now beyond human ability).

What remains alive is the difficult part. Which idealization, which calculation, which spherical cow. In other words, running the full loop of science with AI, not just the calculation in the middle.

That part is still ours. For now.


[^1]: We found some or all of these issues in several benchmarks presented in the paper, and also in our own PHYSICS benchmark, which was not included in the first version of the paper because we did not have time to audit it fully. It will be scrutinized in a future revision.

[^2]: I personally tend to believe that in response to a single prompt, LLMs seem to be finding genuinely creative ideas.
