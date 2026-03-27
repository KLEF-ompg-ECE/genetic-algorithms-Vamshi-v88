# Assignment 2 — Genetic Algorithm: Knapsack Problem
## Observation Report

**Student Name  :** Vamshi krishna  
**Student ID    :** 2310040088  
**Date Submitted:** 2026-03-27  

---

## How to Submit

1. Run each experiment following the instructions below
2. Fill in every answer box — do not leave placeholders
3. Make sure the `plots/` folder contains all required images
4. Commit this README and the `plots/` folder to your GitHub repo

---

## Before You Begin — Read the Code

Open `ga_knapsack.py` and read through it. Then answer these questions.

**Q1. What does the `fitness()` function return? Why does an overweight solution score 0?**

```
The `fitness()` function returns the total value of the packed items if their combined weight is within the maximum limit. If the total weight exceeds the limit, it scores 0 because an overweight knapsack represents an invalid solution that violates the core constraint of the problem. Penalizing it fully heavily discourages the algorithm from keeping such solutions.
```

**Q2. What does `tournament_select()` do? Why are higher-fitness individuals more likely to be chosen?**

```
`tournament_select()` picks a random subset of candidates and selects the one with the highest fitness among them to act as a parent. Higher-fitness individuals are more likely to be chosen because they continually have a higher probability of being the maximum fitness item within any randomly selected tournament group, naturally favoring better traits without exclusively picking the absolute best.
```

**Q3. Look at the `run_ga()` loop. Find this line:**
```python
next_gen = [best_chromosome[:]]
```
**What is this doing? Why is it important to always keep the best solution?**

```
This line implements elitism by unconditionally copying the single best chromosome from the current generation into the next generation. It is highly important to always keep the best solution to guarantee that the highest fitness never decreases across generations, ensuring that exceptionally good traits discovered are not accidentally lost due to adverse crossover or mutation operations.
```

---

## Experiment 1 — Baseline Run

**Instructions:** Run the program without changing anything.
```bash
python ga_knapsack.py
```

**Fill in this table:**

| Metric | Your result |
|--------|-------------|
| Number of generations | 50 |
| Best value at generation 1 | 60 |
| Final best value | 77 |
| Total weight of best solution (kg) | 14.4 |
| Is solution valid (Yes / No) | Yes |

**Copy the printed packing list here:**
```
  Best Packing List
--------------------------------------
  + Water bottle
  + First aid kit
  + Sleeping bag
  + Torch
  + Energy bars (x6)
  + Rain jacket
  + Map & compass
  + Cooking stove
  + Rope (10 m)
  + Sunscreen
  + Power bank
--------------------------------------
```

**Look at `plots/experiment_1.png` and describe what you see (2–3 sentences).**  
*Where does the biggest improvement happen? Does the curve flatten at some point?*
```
The biggest improvement happens in the early generations where the curve rises steeply as the algorithm quickly discovers much better combinations. The curve then noticeably flattens out around the later generations as the algorithm converges on a near-optimal solution and further improvements become rare.
```

---

## Experiment 2 — Effect of Mutation Rate

**Instructions:** In `ga_knapsack.py`, find the `# EXPERIMENT 2` block in `__main__`.  
Copy it three times and run with `mutation_rate` = **0.01**, **0.05**, and **0.30**.  
Save plots as `experiment_2a.png`, `experiment_2b.png`, `experiment_2c.png`.

**Results table:**

| mutation_rate | Final best value | Weight (kg) | Valid? | Shape of curve |
|--------------|-----------------|-------------|--------|----------------|
| 0.01         | 75              | 14.9        | Yes    | Plateaus early |
| 0.05         | 77              | 14.4        | Yes    | Steady climb   |
| 0.30         | 78              | 14.1        | Yes    | Spiky / erratic|

**Compare the three plots. What happens when mutation is too low? Too high? (3–4 sentences)**  
*Hint: Too low = no diversity, may get stuck. Too high = random search. What is the sweet spot?*
```
When the mutation rate is too low (0.01), there is very little genetic diversity, causing the algorithm to get stuck in local optima and failing to find a better solution. When it's too high (0.30), the search effectively becomes excessively random, occasionally destroying good traits and making the improvements unpredictable. A balanced mutation rate sits in the sweet spot (0.05), allowing for steady and stable convergence while maintaining just enough diversity to incrementally improve the generation over time.
```

**Which mutation_rate gave the best result? Why do you think that is?**
```
In this very specific run due to the fixed random seed (42), `mutation_rate = 0.30` technically achieved the highest best value (78) due to highly erratic random jumps. However, `mutation_rate = 0.05` is generally the best setting because it ensures stable and consistent convergence without completely destroying prior progress, acting as a much more reliable approach than pure random searches.
```

---

## Summary

**Complete this table with your best result from each experiment:**

| Experiment | Key setting | Final value | Main finding in one sentence |
|------------|-------------|-------------|------------------------------|
| 1 — Baseline | mutation_rate = 0.05 | 77 | Balanced exploration leads to steady convergence. |
| 2 — Mutation rate | mutation_rate = 0.30 | 78 | High mutation acts like a random search, sometimes lucky but very chaotic. |

**In your own words — what is the most important thing you learned about Genetic Algorithms from these experiments? (3–5 sentences)**
```
The most important thing I learned is that genetic algorithms are incredibly sensitive to their input parameters, especially mutation. While crossover reliably combines the best traits of parent solutions, a well-tuned mutation rate is absolutely crucial to introduce new genes and prevent the population from stagnating. However, finding the right balance—the 'sweet spot'—is essential because setting the mutation rate too high effectively devolves the intelligent algorithm into a highly inefficient random search.
```

---

## Submission Checklist

- [x] Student name and ID filled in
- [x] Q1, Q2, Q3 answered
- [x] Experiment 1: table filled, packing list pasted, plot observation written
- [x] Experiment 2: results table filled (3 rows), observation and answer written
- [x] Summary table completed and reflection written
- [x] `plots/` contains: `experiment_1.png`, `experiment_2a.png`, `experiment_2b.png`, `experiment_2c.png`
