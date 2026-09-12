---
layout: post
title: "Is Physics Dead?"
subtitle: "Expert re-grading, broken benchmarks, and what frontier models can and cannot do in physics"
author: "John Sous"
date: 2026-09-11 12:00:00 -0400
description: "What an expert audit of physics benchmarks reveals about frontier models, evaluation, and the parts of physics that remain difficult."
---

> *Physics is dead. Physics remains dead. And we have killed it.*
>
> Nietzsche, more or less

Anyone who works with frontier models knows two things at once. They can do astonishing things, and they drift. Over a long session they can lose the thread, forget what they have established, and struggle to identify the next useful step in a research project. Both things are true, and anyone who has spent a week with an agent on a hard problem has felt both.

So what about physics?

## The benchmarks said we were safe

If you looked at the leaderboards, physics appeared to be one of the last holdouts. On CritPt, a benchmark of research-level physics challenges, GPT-5.6-Sol scored 32%. On the physics portion of Humanity's Last Exam, it scored 47%. The apparent message was that frontier models still got roughly half of graduate-level physics wrong.

It was tempting to believe that result. Most of the time, the hardest part of physics is not completing a calculation. It is deciding which calculation to do.

There is an old joke about a physicist hired to help a dairy farm who begins with "assume a spherical cow." The joke is on us, but it also captures the craft: physics is the art of finding the idealization that discards almost everything about a problem while preserving exactly what matters.

In 1983, Robert Laughlin wanted to explain the fractional quantum Hall effect. The direct approach would have required solving the Schrödinger equation for a vast number of strongly interacting electrons. Instead, Laughlin guessed a many-electron wavefunction with the right symmetry and limiting behavior. The guess was the discovery.

Kenneth Wilson and Michael Fisher made a similarly audacious move when studying phase transitions. They treated a problem in three spatial dimensions through an expansion around four dimensions, solved it in 4 − ε dimensions, and then set ε = 1. These are not merely calculations. They are decisions about which calculation might expose the underlying physics.

A benchmark problem usually makes that decision in advance. Perhaps the low leaderboard scores meant that even then, physics remained beyond the models.

## What actually happened

We started by trying to understand where the models failed. We collected rejected answers, then handed them to physicists and asked them to check the grading. Faculty and graduate students, mostly at Yale, reviewed problems in their own subfields.

The physicists came back annoyed, and not at the models.

First, the evaluation pipeline was rejecting correct answers written in equivalent forms. In one PHYBench problem about the tension in a rope tied around three balls with a fourth ball on top, the model answered P/(3√6). The reference gave (√6/18)P. These expressions are identical, but the rule-based grader assigned a zero. On PHYBench and PRISM-Physics, grader mistakes were the largest source of rejections.

Second, many benchmark items were defective. We found incorrect arithmetic in reference answers, questions that omitted information needed to choose among the answers, and physics problems whose results depended on unstated conventions. A Kitaev honeycomb model question, for example, did not specify whether the couplings multiply Pauli matrices or spin-1/2 operators, changing the ground-state energy by a factor of four.

Of 250 rejected answers audited across HLE-Physics, PHYBench, PRISM-Physics, and UGPhysics, 238 turned out to be benchmark or grader failures. Only 12 were model failures. On PRISM-Physics there were none; on UGPhysics there was one.

For the two hardest expert-authored benchmarks, we audited every question and repaired problems whenever a defensible repair existed. Thirty of 50 CMT-Benchmark questions had a defect, as did 21 of the 56 CritPt questions we audited. After correcting graders and repairing or excluding flawed questions, the measured results changed sharply:

| Benchmark | Pre-audit mean@4 | Corrected mean@4 | Corrected pass@4 |
| --- | ---: | ---: | ---: |
| PHYBench | 26.5% | 90.2% | 95.4% |
| PRISM-Physics | 13.0% | 94.6% | 96.0% |
| UGPhysics | 83.0% | 92.1% | 93.9% |
| HLE-Physics | 47.3% | 78.7% | 91.4% |
| CMT-Benchmark | 61.0% | 87.2% | 98.0% |
| CritPt | 32.3%* | 87.5% | 94.4% |

*The pre-audit CritPt figure is Artificial Analysis's reported mean@5 on 70 challenges. The corrected results use the 54 retained challenges.*

Claude Fable 5 and Gemini 3.1 Pro moved in the same direction on all six benchmarks.

There are important qualifications. The corrected scores are computed on retained or repaired question sets, so the pre-audit and corrected values do not always use identical questions. For four benchmarks, we audited only questions rejected for GPT-5.6-Sol. Some runs used tools while others did not, and three benchmarks draw from publicly available problems that could appear in training data. Even the best corrected evaluator we tested still had an error rate of about 4%. These details matter, but none changes the central result: the original scores substantially understated model performance.

With apologies to my fellow physicists, AI is killing physics, at least the kind that fits in a problem set. Given several attempts, frontier models now solve nearly all well-posed, closed-ended physics problems in these benchmarks, from undergraduate mechanics to research-adjacent condensed matter theory. The leaderboards suggest otherwise because the leaderboards are broken.

## Does this mean physics is dead?

No. But something did die, and it is worth being precise about what.

Every benchmark has a defect rate: wrong references, ambiguous questions, and graders that fail to recognize equivalent answers. That rate creates a floor beneath the measured error. When models were weak, the floor barely mattered. A model with a 60% true error rate will not reveal a 10% benchmark defect rate.

The true error rate of frontier models has now fallen below the defect rate of essentially every physics benchmark we examined. Once that happens, most errors on the scorecard belong to the benchmark rather than the model. The scorecard stops measuring the model and begins measuring the benchmark's sloppiness.

Grader errors follow the same logic. A faulty grader mostly harms correct answers. A weak model produces few correct answers, so the defect is masked. A strong model produces many, and the grader's errors accumulate. Bad evaluation is hidden by weak models and exposed by strong ones.

This is not unique to physics. It is what happens when the thing being measured outgrows the ruler. Physics benchmarks are especially vulnerable because they are commonly graded against human-written reference solutions without the executable checks available in software benchmarks.

What died is the idea that closed-ended physics problems can tell us much about frontier capabilities. If a benchmark is made of questions that look like homework, it may already be saturated.

## Solving problems is not doing physics

Alongside the audit, we pointed GPT-based agentic systems at several open problems in theoretical physics. We have not fully solved one. The agents made considerably less progress than comparable systems have made on open mathematics problems.

The pattern is more interesting than the headline. These systems are excellent at portions of an open problem that resemble a problem set. Give them a Hamiltonian and a concrete question, and they can set up the calculation, perform perturbation theory, run numerics, and check limits. What they do poorly is choose the calculation.

When a standard approach fails, as it often must on a genuinely open problem, agents tend to try a neighboring standard approach and then another. Over a long session, the work spreads into many individually reasonable partial calculations that do not add up to an attack on the actual question. The mistakes are often not algebraic. They lie in the setup, in deciding what to retain and what to discard.

They are, in other words, in the spherical cow.

That is the skill represented by Laughlin's guess and Wilson and Fisher's imaginary dimensions. A closed-ended benchmark has already selected an idealization. On an open problem, nobody has made that choice yet.

This observation is preliminary. It comes from a handful of problems and harnesses, and mathematical successes have also required long runs with humans in the loop. Still, the contrast points toward a verifier problem. A proof can be checked line by line. A physical idea is ultimately checked by how well it explains the world, and the world does not return a boolean.

## Same question, four answers

The gap between mean@4 and pass@4 deserves attention. On HLE-Physics, GPT-5.6-Sol answered 79% correctly on average across four attempts but solved 91% at least once. On CMT-Benchmark, the figures were 87% and 98%. What should we make of a system that gives different answers to the same question?

One response is practical. A model sampled at nonzero temperature is a distribution over solutions, not a calculator. In this view, pass@k measures capability while mean@k measures reliability. Verification, independent attempts, self-consistency, and better agent scaffolding can narrow the gap.

The less comfortable response is that wrong attempts do not reliably come with lower confidence. Some errors are slips: one attempt drops a factor and another does not. More samples can help. Others are systematic. On one CritPt challenge involving two optically trapped nanoparticles, every attempt assumed the polarizabilities were real even though the problem did not say so. Resampling did not fix the mistaken model of the problem.

The distinction matters. Slips are a reliability problem; systematic misreadings are a physics problem. A responsible evaluation should report both average success and best-of-several capability, then investigate which errors produce the difference.

## What comes next

**Harder tasks, defined by the community.** The next generation of evaluations should include tasks that are hard in the way physics is hard, where choosing the idealization is part of the problem and there may be no single reference answer. Building them will require expert curation, clear conventions, and serious verification.

**Open challenges.** To learn whether models can do physics rather than physics homework, we should give them open problems and document the attempts publicly, with physicists in the loop. Partial progress and instructive failure should both count as useful outcomes.

**Better agents and harnesses for physics.** Physics needs verification tools built around its own habits: limiting cases, dimensional analysis, agreement with known results, numerical sanity checks, and the questions a good advisor asks at a whiteboard. The best first targets may not be famous grand challenges, but problems that are real while keeping the space of plausible idealizations small.

## What died, and what did not

Physicists have said for some time that leaderboard scores do not match what they see when using frontier models. The audit puts numbers behind that intuition. What died is a way of measuring physics ability, along with the comfortable belief that these systems still struggle broadly with problem sets.

What remains alive is the difficult part: which idealization, which calculation, which spherical cow.

That part is still ours. For now.
