# MA 213 Tutorial Development Plan

This plan develops the tutorial sequence on top of the current lecture, lab, and learning-objective structure. The tutorials are designed as short pre-lab experiences: students should arrive at lab having already seen the core R tools, so lab time can focus on interpretation, debugging, and statistical reasoning.

## Tutorial Design Pattern

Each tutorial should follow the same structure so students know what to expect.

1. **Orientation:** State the statistical purpose of the tutorial and connect it to the next lab.
2. **Worked examples:** Introduce the R tools with small examples that students can modify.
3. **Your turn exercises:** Ask students to complete similar tasks with less scaffolding.
4. **Interpretation prompts:** Require short written answers in context, not just code output.
5. **Submission check:** End with a small completion item or hash, matching the existing learnr workflow.

Recommended tutorial length: 35-55 minutes.

Recommended coding load: 8-14 short exercises, with no single exercise depending on too many hidden steps.

## Sequence Overview

| Tutorial | Current status | Prepares students for | Main R focus | Main statistical focus |
| --- | --- | --- | --- | --- |
| Tutorial 1 | Existing lesson | Lab 2 | R basics, vectors, subsetting | Variables and data structure |
| Tutorial 2 | Existing lesson | Lab 2 | Importing data, `dplyr`, missing values | Data cleaning and summaries |
| Tutorial 3 | Existing lesson | Lab 3 | `ggplot2`, plot choice, grouped summaries | Visualizing distributions and associations |
| Tutorial 4 | Existing lesson | Lab 4 | Functions, loops, repeated calculation | Probability models, expected value, and variance |
| Tutorial 5 | Existing lesson | Lab 5 | Simulation, sample means, reusable simulation functions | LLN, CLT, and sampling distributions |
| Tutorial 6 | Existing lesson | Lab 6 | Confidence intervals, p-values, chi-square tables | Inference for proportions and categorical data |
| Tutorial 7 | New lesson | Lab 7 | Prior, likelihood, posterior, grid approximation | Bayesian updating and interpretation |

## Tutorial 1: R Basics and Data Objects

**Folder:** `01-lesson`  
**Prepares for:** Lab 2  
**Primary objectives:** M1 LO1, M1 LO3, M6 LO1, M6 LO2

### Tutorial purpose

Tutorial 1 gives students a low-stakes first contact with R. The goal is not to make students fast programmers; it is to make them comfortable reading simple R commands, storing values, creating vectors, and extracting pieces of data.

### Existing strengths

- Introduces R as a calculator before moving to objects.
- Uses vectors and subsetting, which supports later data-frame work.
- Includes several "Your turn" exercises and a submission section.

### Suggested development

- Add a short variable-type checkpoint: ask students to classify examples as numerical, categorical, ordinal, or identifier variables.
- Add one exercise where students intentionally make a small error, read the error message, and fix it.
- Add a final interpretation prompt: "What is the difference between assigning a value and printing a value?"

### Suggested exercise flow

1. Load packages and confirm the tutorial environment.
2. Use R as a calculator.
3. Assign and print numeric and character values.
4. Create vectors.
5. Access vector elements by position.
6. Subset vectors using logical conditions.
7. Classify simple variables.
8. Submit completion item.

## Tutorial 2: Data Wrangling with `dplyr`

**Folder:** `02-lesson`  
**Prepares for:** Lab 2  
**Primary objectives:** M1 LO1, M1 LO3, M1 LO4, M6 LO1, M6 LO2

### Tutorial purpose

Tutorial 2 moves from isolated R objects to real data frames. Students should leave able to import a data set, inspect its structure, create new variables, remove missing values when appropriate, and produce small tables that support interpretation in Lab 2.

### Existing strengths

- Uses the New York air quality data, which is small enough for beginners.
- Introduces the pipe, `mutate()`, `case_when()`, contingency tables, and missing values.
- Ends with a multi-step exercise that combines cleaning, categorizing, and tabulating.

### Suggested development

- Add a short "before and after" check after each transformation so students see that code changes the data object.
- Add a prompt distinguishing `filter()` from `select()`, since students often confuse row and column operations.
- Add an interpretation prompt after the wind/ozone contingency table: "What pattern do you see, and what should we be careful not to claim?"

### Suggested exercise flow

1. Load packages.
2. Import and inspect `airquality.csv`.
3. Use the pipe to chain simple operations.
4. Create a categorical variable with `mutate()` and `case_when()`.
5. Build one-way and two-way tables.
6. Identify and remove missing values when justified.
7. Complete a multi-step wind and ozone categorization task.
8. Submit completion item.

## Tutorial 3: Data Visualization with `ggplot2`

**Folder:** `03-lesson`  
**Prepares for:** Lab 3  
**Primary objectives:** M1 LO1, M1 LO3, M1 LO4, M6 LO1

### Tutorial purpose

Tutorial 3 helps students choose plots based on variable type and research question. The coding goal is to make basic `ggplot2` graphics; the statistical goal is to describe distributions and associations accurately.

### Existing strengths

- Introduces the `ggplot()` template explicitly.
- Uses several plot types: dot plots, box plots, histograms, scatterplots, bar plots, and pie charts.
- Includes both numerical and categorical examples using `airquality` and `Titanic`.

### Suggested development

- Add a "choose the plot" checkpoint before students write code.
- Add reminders that histograms and box plots describe one numerical variable, while scatterplots describe two numerical variables.
- Add a short caution after the pie chart section: pie charts can be useful for rough composition, but bar plots are usually easier to compare.

### Suggested exercise flow

1. Load packages.
2. Practice the `ggplot(data, aes(...)) + geom_*()` template.
3. Visualize one numerical variable with dot plots, box plots, and histograms.
4. Adjust histogram bins and labels.
5. Visualize two numerical variables with a scatterplot.
6. Visualize one categorical variable with a bar plot.
7. Visualize two categorical variables with grouped or filled bars.
8. Complete a final filtered-ozone visualization task.
9. Submit completion item.

## Tutorial 4: Functions, Loops, and Probability Calculations

**Folder:** `04-lesson`  
**Prepares for:** Lab 4  
**Primary objectives:** M2 LO1, M2 LO3, M2 LO4, M2 LO5, M6 LO1, M6 LO2

### Tutorial purpose

Tutorial 4 should teach students how repeated calculations become reusable code. It should connect functions and loops to probability rather than treating them as abstract programming topics.

### Proposed content

- Define a simple function with one input and one output.
- Use a function to compute a probability from counts.
- Use a function to compute expected value from values and probabilities.
- Use `for` loops or `replicate()` to repeat a random experiment.
- Compare theoretical probability with simulated probability.

### Recommended data and examples

- Dice rolls or coin flips for discrete sample spaces.
- A small custom probability distribution for expected value and variance.
- Binomial examples using `rbinom()`, `dbinom()`, and `pbinom()`.

### Suggested exercise flow

1. Write a function that converts counts to proportions.
2. Check whether a probability distribution is valid.
3. Compute expected value from a table of outcomes and probabilities.
4. Simulate one random outcome with `sample()`.
5. Repeat the simulation many times with `replicate()`.
6. Summarize simulated outcomes with a table or plot.
7. Compare simulated results to theoretical results.
8. Submit a short explanation of why simulation improves as repetitions increase.

### Suggested final task

Students create a function called `expected_value()` that takes a vector of outcomes and a vector of probabilities, checks that the probabilities sum to 1, and returns the expected value.

## Tutorial 5: LLN, CLT, and Sampling Distributions

**Folder:** `05-lesson`  
**Prepares for:** Lab 5  
**Primary objectives:** M2 LO2, M2 LO6, M3 LO1, M3 LO2, M6 LO1, M6 LO3

### Tutorial purpose

Tutorial 5 should bridge probability and sampling distributions. Students should see that a sample statistic varies from sample to sample, that larger samples produce less variable sample means, and that the CLT makes sampling distributions useful even when the population is skewed.

### Proposed content

- Draw repeated samples from a known population.
- Compute a sample mean for each sample.
- Plot the sampling distribution.
- Compare small and large sample sizes.
- Compare the number of repetitions `K` with the sample size `n`.
- Connect simulated spread to standard error.

### Recommended data and examples

- Simulated right-skewed populations using `rgamma()` or `rexp()`.
- Optional comparisons with normal, binomial, Poisson, exponential, and gamma populations.
- Base R and tidyverse tools, especially `sample()`, `replicate()`, and `ggplot()`.

### Suggested exercise flow

1. Simulate one sample and compute a point estimate.
2. Repeat sampling many times.
3. Plot the distribution of point estimates.
4. Change the sample size and compare variability.
5. Compute a standard error for a sample mean.
6. Write a reusable simulation function.
7. Compare `n = 10`, `n = 30`, and `n = 100`.
8. Submit a written explanation of LLN/CLT behavior.

### Suggested final task

Students investigate how sample size changes the center, spread, and shape of a sampling distribution, then write two sentences explaining the pattern in context.

## Tutorial 6: Confidence Intervals and Hypothesis Tests

**Folder:** `06-lesson`  
**Prepares for:** Lab 6  
**Primary objectives:** M3 LO3, M3 LO4, M3 LO5, M4 LO1, M4 LO2, M6 LO1, M6 LO3

### Tutorial purpose

Tutorial 6 should prepare students for the inference lab by making the relationship between confidence intervals and hypothesis tests explicit. It should also give students a first structured pass at two-way tables for chi-square inference.

### Suggested content

- Construct and interpret a confidence interval for one proportion.
- State a null hypothesis and compute a p-value for one proportion.
- Simulate confidence interval coverage.
- Build two-way tables from categorical counts.
- Use `chisq.test()` and interpret the output cautiously.

### Suggested final task

Students test whether two categorical variables appear independent in the Titanic data and write one sentence interpreting the p-value in context.

## Tutorial 7: Bayesian Updating

**Folder:** `07-lesson`  
**Prepares for:** Lab 7  
**Primary objectives:** M5 LO1, M5 LO2, M5 LO3, M6 LO4

### Tutorial purpose

Tutorial 7 should prepare students for the Bayesian lab by making the prior-likelihood-posterior workflow concrete before lab. The tutorial should emphasize interpretation, not advanced theory.

Suggested content:

- Define prior beliefs for a binary outcome.
- Use a likelihood from observed successes and failures.
- Update to a posterior using the beta-binomial model.
- Compare weak and strong priors.
- Explain how Bayesian evidence accumulates.

Suggested final task:

Students compare two priors using the same data and explain how the posterior changes.

## Implementation Priorities

1. Finish the conceptual scope of Tutorials 5-7 before polishing style.
2. Keep the learnr template consistent across all seven tutorials.
3. Reuse the completion/hash pattern already present in Tutorials 1-6.
4. Give each tutorial at least one interpretation prompt that is graded or checked.
5. Avoid making tutorials into full labs; the tutorial should prepare students for the lab, not replace it.

## Alignment Check

| Course component | Tutorial support |
| --- | --- |
| Project 1 | Tutorials 1-3 support data cleaning, visualization, and presentation preparation. |
| Project 2 | Tutorials 5-7 support inference, Bayesian reasoning, and written explanation. |
| Quizzes 1-2 | Tutorials 1-4 support variable types, EDA, probability, and distributions. |
| Quizzes 3-4 | Tutorials 5-6 support sampling distributions, confidence intervals, and hypothesis tests. |
| Quiz 5 | Tutorial 7 supports Bayesian reasoning and comparison of inferential perspectives. |
