# MA213-tutorials

Interactive tutorials developed with the `learnr` package.

## Tutorial Sequence

| Tutorial | Folder | Prepares for | Focus |
| --- | --- | --- | --- |
| 1 | `01-lesson` | Lab 2 | R basics, data objects, vectors, and subsetting |
| 2 | `02-lesson` | Lab 2 | Data import, cleaning, transformation, and summaries |
| 3 | `03-lesson` | Lab 3 | Data visualization with `ggplot2` |
| 4 | `04-lesson` | Lab 4 | Functions, repeated calculations, and probability simulation |
| 5 | `05-lesson` | Lab 5 | LLN, CLT, and sampling distributions |
| 6 | `06-lesson` | Lab 6 | Confidence intervals, hypothesis tests, and chi-square setup |
| 7 | `07-lesson` | Lab 7 | Bayesian updating and posterior interpretation |

Each lesson folder contains the source `.Rmd` tutorial and a rendered
`.html` file.

## Instructor Manual

The editable source for each tutorial is the `.Rmd` file inside its
lesson folder, for example `01-lesson/01-01-lesson.Rmd`. The `.html`
file is the rendered student-facing tutorial. Edit the `.Rmd` first,
then render it again to update the `.html`.

### Basic Editing Workflow

1. Open the lesson `.Rmd` file you want to change.
2. Edit the question text, exercise chunk, hint chunk, or solution
   block.
3. Knit or render the `.Rmd` file.
4. Open the rendered `.html` tutorial and test the changed exercise.

In RStudio, use the **Run Document** or **Knit** button. From R, you can
also render a lesson with:

```r
rmarkdown::render("01-lesson/01-01-lesson.Rmd")
```

### Adding or Editing a Question

Most student exercises use a learnr exercise chunk:

````markdown
### Question title

Write the instructions students should see.

```{r ex-new-topic, exercise=TRUE}
# Optional starter code goes here
```
````

To edit an existing question, change the heading, instructions, or the
starter code inside the `exercise=TRUE` chunk.

Use a unique chunk label for every exercise, such as `ex-mean-income` or
`plot-histogram-1`. Do not reuse a label that already appears in the
same `.Rmd` file.

### Adding or Editing Hints

Hints are ordinary R chunks placed after the exercise. They should use a
label related to the exercise:

````markdown
```{r ex-new-topic-hint-1}
# Think about which object contains the values you need.
```

```{r ex-new-topic-hint-2}
# Try: mean(data$variable)
```
````

To edit a hint, change the text or code inside the hint chunk. To add
more hints, add another chunk with a new label such as
`ex-new-topic-hint-2`.

### Adding or Editing Timed Solutions

Timed solutions are created with the helper function `timed_solution()`
in a server-context chunk. The solution is displayed through a matching
`uiOutput()` chunk.

````markdown
```{r, context="server", echo=FALSE}
timed_solution(
  "ex_new_topic_solution_code",
  "answer <- mean(data$variable)\nprint(answer)"
)
```

```{r ex-new-topic-solution-ui, echo=FALSE}
uiOutput("ex_new_topic_solution_code")
```
````

When adding a solution:

- Use a unique output id, such as `ex_new_topic_solution_code`.
- Use the same output id in both `timed_solution()` and `uiOutput()`.
- Put `\n` inside the solution string where the displayed code should
  move to a new line.
- Keep the server chunk label blank or unique. The `uiOutput()` chunk
  should have a unique label ending in `-solution-ui`.

To edit a solution, change the code string inside `timed_solution()`.

Some older lessons may also include a regular chunk such as
`{r ex2-solution}`. Those chunks are visible learnr solution/support
chunks. For the current timed-release style, prefer the
`timed_solution()` plus `uiOutput()` pattern.

### Changing the Solution Reveal Time

Each lesson defines a reveal time near the top of the setup chunk:

```r
my_reveal_time <- "2026-06-20 15:00:00"  # solution reveal time
```

Change this value to the desired release date and time. The helper uses
the `America/New_York` time zone by default.

### Adding Non-Code Checkpoints

For short-answer prompts, classification questions, or reflection
questions, you can still use an exercise chunk and place comments as
prompts:

````markdown
```{r variable-type-checkpoint, exercise=TRUE}
# student_id:
# final_exam_score:
# class_year:
```
````

This gives students a place to type their answer while keeping the
prompt visible.

### Common Things to Check Before Publishing

- The `.Rmd` renders without errors.
- Every chunk label is unique.
- Every `timed_solution()` output id matches its `uiOutput()` id.
- The reveal time is correct for the class schedule.
- Hints appear in the intended order.
- Starter code runs or intentionally produces the error students are
  asked to fix.
- The rendered `.html` file is updated after changes.
