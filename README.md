# Continuous Lipschitz Bandits

An academic project exploring regret bounds for **continuous multi-armed bandit problems with Lipschitz reward functions**, completed for the **High-Dimensional Probability** course at Sharif University of Technology.

> ## 👥 Collaborative Academic Project
>
> **This project was completed collaboratively and was not solely my work.**
>
> **Authors**
>
> - **Mehdi Darabi**
> - **Hami Ebadzadeh Semnani**
>
> I am publishing the project here as part of my personal academic portfolio. Its presence on my GitHub account should not be interpreted as a claim that the report, presentation, or mathematical work was completed by me individually.

---

## Quick Links

📄 **[Read the Final Report](./report/lipschitz-continuum-bandits-report.pdf)**

📊 **[Open the Final Presentation](./presentation/lipschitz-continuum-bandits-presentation.pdf)**

📐 **[Report LaTeX Source](./report/source/main.tex)**

🎞️ **[Presentation LaTeX Source](./presentation/source/main.tex)**

---

## Project Overview

The classical multi-armed bandit problem asks an agent to repeatedly choose among uncertain actions while balancing two competing goals:

- **exploration** — learning more about actions whose rewards are uncertain;
- **exploitation** — choosing actions that currently appear to perform well.

This project studies a continuous version of that problem. Instead of choosing from finitely many arms, the action space is a continuous set such as

\[
\mathcal{X}=[0,1]^d,
\]

and the expected reward is described by an unknown function

\[
f:\mathcal{X}\rightarrow[0,1].
\]

We assume that \(f\) is Lipschitz, so nearby actions cannot have arbitrarily different expected rewards. The main question of the project was whether this geometric structure could be used to obtain useful regret bounds for a continuous bandit problem.

The work develops two different approaches. The first produces a concrete bound by discretizing the action space and applying UCB1. The second investigates a more probabilistic route involving the expected supremum of a stochastic process, but ultimately does not produce a useful regret bound.

---

## Background: UCB1

For a finite \(K\)-armed bandit, UCB1 assigns each arm an index combining its empirical reward with an uncertainty bonus:

\[
I_i(t)
=
\widehat{\mu}_i(t-1)
+
\sqrt{\frac{2\log t}{T_i(t-1)}}.
\]

The first term favors arms that have performed well, while the second encourages exploration of arms that have been sampled less frequently.

The project starts from the classical finite-arm regret analysis and then asks how this idea can be adapted to a continuous action space.

---

## Attempt 1 — Discretization with an \(\varepsilon\)-Cover

The first approach replaces the continuous action space with a finite \(\varepsilon\)-net

\[
N_\varepsilon \subset \mathcal{X}.
\]

UCB1 can then be run on the points of this finite set.

The regret can be separated into two sources:

1. **discretization error**, because the best point in the \(\varepsilon\)-net may not be the true continuous optimum;
2. **bandit regret**, produced by learning which point in the finite net is best.

Lipschitz continuity gives

\[
f^\ast-f^\ast_\varepsilon \leq L\varepsilon,
\]

so the accumulated discretization error is at most \(L\varepsilon n\).

For \(\mathcal{X}=[0,1]^d\), an \(\varepsilon\)-cover has approximately

\[
K_\varepsilon \asymp \varepsilon^{-d}
\]

points. Combining the discretization error with a gap-independent UCB1 bound gives a regret estimate of the form

\[
R(n)
\leq
L\varepsilon n
+
4\sqrt{2K_\varepsilon n\log n}
+
\left(1+\frac{\pi^2}{3}\right)K_\varepsilon.
\]

Choosing

\[
\varepsilon=n^{-1/(d+2)}
\]

leads to the dominant rate

\[
R(n)
=
O\!\left(
n^{\frac{d+1}{d+2}}\sqrt{\log n}
\right),
\]

up to lower-order terms and constants.

This was the productive direction developed in the project.

---

## Attempt 2 — Supremum of a Stochastic Process

A second idea was motivated by bounds on quantities such as

\[
\mathbb{E}\left[\sup_{x\in\mathcal{X}} Z_x\right]
\]

for centered Lipschitz sub-Gaussian processes.

The hope was to construct a process \(Z_x\) whose expected supremum controlled bandit regret, allowing covering-number tools from high-dimensional probability to be used directly.

A natural candidate preserved the Lipschitz dependence on \(x\), but it was not centered. Centering it removed the dependence on \(x\), making the supremum argument ineffective.

As a result, this route did not improve on the trivial \(O(n)\) regret bound.

The report deliberately keeps this unsuccessful attempt because it documents both the motivation and the mathematical obstruction encountered.

---

## Why This Was an HDP Project

The connection to High-Dimensional Probability comes primarily through geometric and probabilistic tools such as:

- metric spaces and Lipschitz functions;
- \(\varepsilon\)-nets and covering numbers;
- gap-independent regret analysis;
- sub-Gaussian random variables and processes;
- expected suprema of stochastic processes;
- the interaction between dimension, covering complexity, and statistical learning.

The project therefore sits at the intersection of **probability, online learning, optimization, and high-dimensional geometry**.

---

## Repository Structure

```text
.
├── README.md
├── .gitignore
│
├── report/
│   ├── lipschitz-continuum-bandits-report.pdf
│   │
│   └── source/
│       ├── main.tex
│       ├── refs.bib
│       └── Shariflogo.png
│
└── presentation/
    ├── lipschitz-continuum-bandits-presentation.pdf
    │
    └── source/
        ├── main.tex
        └── figs/
            ├── ladders_carpet.png
            └── octopus.png
```

### `report/`

Contains the final written report.

### `report/source/`

Contains the XeLaTeX source, bibliography, and assets used to produce the report.

### `presentation/`

Contains the final 31-slide Beamer presentation.

### `presentation/source/`

Contains the original Beamer source and its figures.

---

## Tools & Topics

- **High-Dimensional Probability**
- **Multi-Armed Bandits**
- **UCB1**
- **Online Learning**
- **Lipschitz Functions**
- **Covering Numbers / \(\varepsilon\)-Nets**
- **Sub-Gaussian Processes**
- **Regret Analysis**
- **LaTeX / XeLaTeX**
- **Beamer**

---

## Academic Context

**Course:** High-Dimensional Probability  
**University:** Sharif University of Technology  
**Instructor:** Dr. Mohammad Hossein Yassaee Meybodi

The project was completed as course work and is preserved here as part of my academic portfolio.

The repository keeps the final submitted artifacts together with their original LaTeX sources so that readers can either quickly inspect the finished work or examine the mathematical source in detail.

---

## Reference

The finite-arm UCB1 analysis used in the project is based on:

> Peter Auer, Nicolò Cesa-Bianchi, and Paul Fischer.  
> *Finite-time Analysis of the Multiarmed Bandit Problem*.  
> Machine Learning, 47(2–3):235–256, 2002.

---

## Authorship and Attribution

The original report lists:

- **Mehdi Darabi**
- **Hami Ebadzadeh Semnani**

as its authors.

The presentation likewise identifies the project as collaborative work by the same two participants.

This repository is hosted on my personal GitHub account for portfolio purposes. **Nothing in this repository should be interpreted as a claim that I completed the project independently.**

---

## Start Here

For the complete mathematical development:

### **📄 [Read the Final Report](./report/lipschitz-continuum-bandits-report.pdf)**

For a shorter overview:

### **📊 [Open the Final Presentation](./presentation/lipschitz-continuum-bandits-presentation.pdf)**
