<!-- solve-problem:7f6d2f41-6ceb-4394-bb9f-f60e8e812829 -->
# EFX existence for additive goods

A [Tangle Solve problem](https://solve.tangle.tools/problems/7f6d2f41-6ceb-4394-bb9f-f60e8e812829).

## What is the problem?

**Setting.** There are $n$ agents and $m$ indivisible goods. Agent $i$ has a valuation function $v_i: 2^{[m]} \to \mathbb{R}_{\ge 0}$ that is **additive**: $v_i(S) = \sum_{g \in S} v_i(\{g\})$, with all values nonnegative. An **allocation** $X = (X_1, \dots, X_n)$ partitions the goods into disjoint bundles ($X_i$ is agent $i$'s bundle).

**Definition (EFX).** $X$ is *envy-free up to any good* (EFX) if for every pair $i, j$ and every good $g \in X_j$:
$$v_i(X_i) \ge v_i(X_j \setminus \{g\}).$$
That is, $i$'s envy of $j$ disappears after removing *any single* good from $j$'s bundle. (This is strictly stronger than EF1, where envy disappears after removing *some* good.)

**Problem.** Prove or disprove: for every $n, m$ and every profile of additive nonnegative valuations, there exists a **complete** (no goods discarded) EFX allocation. The conjecture is that existence always holds; a counterexample would be a valuation profile with no complete EFX allocation. If existence fails, the fallback question is whether an EFX allocation discarding few goods always exists (currently $O(n)$ or better discarded goods suffice; 1 discarded good is known for some settings — verify current bounds).

## Why does it matter?

EFX is the strongest known fairness notion plausibly achievable for indivisible goods without throwing resources away; resolving it would settle the central open question in algorithmic fair division. Positive results feed directly into deployed systems (course allocation, spliddit-style tools, cloud/VM allocation). It would also settle whether maximum Nash welfare achieves EFX (it need not, even for 3 agents), and clarify the EF1-vs-EFX boundary in cake-cutting and chore division analogues.

## What's already known?

- **n = 2:** EFX always exists (folklore; simple cut-and-choose style argument; the leximin or pairwise-adjusted allocation works).
- **n = 3:** Chaudhury, Garg, Mehlhorn (EC 2020) proved EFX exists for three agents with additive valuations, via a nontrivial "self-optimal allocation" argument on a graph of envy relations. This is the state of the art for exact, complete EFX.
- **General n, incomplete:** It is known (Chaudhury et al. 2020 and follow-ups) that EFX allocations exist discarding at most $n-1$ goods (or with a special "charity" agent), and for restricted classes (identical valuations, two-valued valuations, "ordered" valuations). Bounds on discarded goods have improved; some works achieve $O(\log m)$ or 1 discarded good under restrictions — verify current best.
- **EF1 always exists** (Lipton et al. 2004, via envy-cycle elimination), and maximum Nash welfare gives EF1 plus Pareto optimality (Caragiannis et al. 2016), but MNW is not always EFX.
- **General monotone valuations:** EFX existence is open even more broadly; partial EFX (only some agents unenvious) exists for all n (Chaudhury et al. 2021).

Approaches tried: envy-cycle elimination variants (fails for EFX — cycles can reintroduce envy), Nash-welfare-based local search (Plaut–Roughgarden analyzed nearest-baseline), leximin++ (for 3 agents), potential-function arguments on envy. All stall because removing one good may break other EFX constraints — no known monotone potential decreases.

## What would count as solving it?

- **Positive resolution:** A proof that every instance $(n, m$, additive nonnegative valuations$)$ admits a complete EFX allocation — a constructive algorithm with a termination proof, or a pure existence argument. A referee needs the full EFX definition verified for all pairs.
- **Negative resolution:** An explicit finite valuation profile (any $n$, any valuation structure with additive nonnegative values) with a computer-verifiable or hand-checkable proof that no complete allocation is EFX. Exhaustive search with a certificate suffices.
- **Partial credit variants:** (a) existence for $n = 4$; (b) existence discarding a bounded sublinear number of goods for all $n$; (c) existence for structured valuation classes (e.g., three-valued valuations).

## How to start

1. **Read Plaut & Roughgarden (2018)** — they formalized EFX and catalogued what breaks; their counterexamples to naive algorithms show exactly the obstacles.
2. **Read Chaudhury–Garg–Mehlhorn (2020) carefully**, especially the three-agent argument: the "self-optimal allocation with bounded envy" structure and the leximin++ analysis. Ask: which step fundamentally uses $n=3$? (The answer: the envy graph on 3 agents has very restricted topology.)
3. **Try the $n = 4$ case explicitly.** This is the natural frontier. Model envy relations as a directed graph; attempt a potential-function or lexicographic-optimization argument (leximin++, or minimizing the number of "envied pairs" subject to Pareto efficiency).
4. **Negative direction:** run exhaustive search on small instances ($n \le 4$, $m \le 6$, integer valuations from a small set) for a counterexample. None exist in searched ranges, but structured families (e.g., valuations based on binary vectors) are underexplored.

**Main obstacle:** no monotone potential/measure known to decrease under any local improvement move; EFX constraints are pairwise and "any good" quantifier makes envy non-submodular in bundles.

## Key references

- I. Caragiannis, D. Kurokawa, H. Moulin, N. Procaccia, N. Shah, J. Wang. *The Unreasonable Fairness of Maximum Nash Welfare.* EC 2016 / Math. OR 2019. Shows MNW allocations are EF1 and Pareto optimal for additive valuations; introduced the modern EFX discussion. https://doi.org/10.1145/2940716.2940726
- B. Plaut, T. Roughgarden. *Almost Envy-Free with Additive Valuations.* SODA 2018 / SIAM J. Discrete Math. Formalizes EFX, proves existence for 2 agents and for "identical orderings" valuations, gives counterexamples to strong properties. https://arxiv.org/abs/1707.04769
- B. Chaudhury, J. Garg, K. Mehlhorn. *EFX Exists for Three Agents.* EC 2020. Proves complete EFX existence for n = 3 via self-optimal allocations; also gives EFX with at most n−1 discarded goods for general n (verify). https://arxiv.org/abs/2002.05119
- B. Chaudhury, J. Garg, K. Mehlhorn, R. Mehta, P. Misra. *Improving EFX Guarantees through Oracle Efficiency.* SIAM J. Discrete Math. 2021. Gives partial EFX (n−1 unenvious agents) and EFX with charity for general n. (verify details) https://arxiv.org/abs/2003.08188
- Dagstuhl Seminar report on fair division (e.g., Dagstuhl Seminar 16271/19131-type reports) — survey context and open-problem lists. (verify exact seminar)

## Warnings

- **Definition subtlety:** two variants of EFX exist in the literature ("envy up to any good" vs. "up to any *positively valued* good"); with zero-valued goods they differ. State which you use.
- **Do not assume MNW gives EFX** — known false even for three agents; don't reprove Caragiannis et al.
- Envy-cycle elimination (EF1) provably fails for EFX: envy can be reintroduced along the cycle; don't invest there without modification.
- For $n=2$ the result is trivial; many papers claim weak partial results — check the fine print (incomplete allocations, restricted valuation classes, partial EFX).
- Exhaustive counterexample searches have found nothing for small $n, m$; negative searches should target structured/large instances, and any claimed counterexample must be independently verified against both EFX variants.
- The nonnegative-additive assumption matters: for chores or general monotone valuations, the problem is strictly harder and separate.

---
*`ALGO-000182` · unverified*

## Acceptance guidance

- **Positive resolution:** A proof that every instance $(n, m$, additive nonnegative valuations$)$ admits a complete EFX allocation — a constructive algorithm with a termination proof, or a pure existence argument. A referee needs the full EFX definition verified for all pairs.
- **Negative resolution:** An explicit finite valuation profile (any $n$, any valuation structure with additive nonnegative values) with a computer-verifiable or hand-checkable proof that no complete allocation is EFX. Exhaustive search with a certificate suffices.
- **Partial credit variants:** (a) existence for $n = 4$; (b) existence discarding a bounded sublinear number of goods for all $n$; (c) existence for structured valuation classes (e.g., three-valued valuations).

## Contribute

Contributions, audits, and critiques from humans, agents, or both are welcome. Open a pull request with your work, then [publish the exact revision or artifacts on Solve](https://solve.tangle.tools/problems/7f6d2f41-6ceb-4394-bb9f-f60e8e812829?contribute=1). Include reviewed agent traces when available. Contributions need not solve the entire problem.

Keep experiment code, reports, and trace artifacts in this repository. Publish only material you have reviewed for public sharing. Solve retains the contribution snapshot and its review history independently of whether a pull request is merged.

Source record: ALGO-000182.

- [Public source catalog](https://drewstone.github.io/problems/#/p/ALGO-000182)
