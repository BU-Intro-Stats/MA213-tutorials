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

## Instructor Editing Guide

Edit the source `.Rmd` file inside each lesson folder, then render the
file again to update the student-facing `.html` tutorial.

For example:

```r
rmarkdown::render("01-lesson/01-01-lesson.Rmd")
```

### 1. How to Make a Quiz

Use `quiz()`, `question()`, and `answer()` in a chunk with
`echo=FALSE`. Mark the correct answer with `correct = TRUE`.

````markdown
```{r variable-type-multiple-choice, echo=FALSE}
quiz(
  question(
    "Which value should usually be stored as character data in R?",
    answer("98.5"),
    answer("\"BU Terrier\"", correct = TRUE),
    answer("TRUE"),
    answer("FALSE"),
    allow_retry = TRUE
  )
)
```
````

Use a unique chunk label, such as `variable-type-multiple-choice`.

### 2. How to Make an Exercise

Use an R chunk with `exercise=TRUE`. Anything inside the chunk appears
as starter code for students.

````markdown
### Assign numeric value 655 to the variable named `number` and print it

```{r ex1, exercise=TRUE}
# Students write their answer here
```
````

To provide starter code, place it inside the exercise chunk:

````markdown
```{r fix-vector-error, exercise=TRUE}
broken_numbers <- c(2, 4, 6, 8
broken_numbers
```
````

Every exercise chunk needs a unique label, such as `ex1`,
`fix-vector-error`, or `subset-ex1`.

### 3. How to Give a Hint

Place a regular R chunk immediately after the exercise. Use a related
label ending in `-hint-1`, `-hint-2`, and so on.

````markdown
```{r ex1-hint-1}
variable_name <- value
```

```{r ex1-hint-2}
variable_name = value # This also works
```
````

Hints are shown through the learnr exercise interface. Keep hints short:
the first hint should nudge students, and later hints can be more
specific.

### 4. How to Give a Solution With Reveal Time

Each lesson has a reveal time near the top of the setup chunk:

```r
my_reveal_time <- "2026-09-20 15:00:00"  # solution reveal time
```

Change this date and time when you want all timed solutions in that
lesson to become visible. The helper uses `America/New_York` by default.

Add the solution using `timed_solution()` in a server-context chunk,
then display it with a matching `uiOutput()` chunk.

````markdown
```{r, context="server", echo=FALSE}
timed_solution(
  "ex1_solution_code",
  "number <- 655\nprint(number)"
)
```

```{r ex1-solution-ui, echo=FALSE}
uiOutput("ex1_solution_code")
```
````

Important details:

- The output id must match exactly in both places:
  `ex1_solution_code`.
- Use `\n` inside the solution string to create a new line.
- Use a unique label for the UI chunk, usually ending in
  `-solution-ui`.

### 5. How to Prepare Variables Without Showing Them to Students

Learnr exercises run in separate environments. If an exercise needs an
object such as `A`, define it in a hidden setup chunk and connect that
setup chunk to the exercise using `exercise.setup`.

````markdown
```{r print-values-setup, include=FALSE}
A <- 10
```

```{r print-values, exercise=TRUE, exercise.setup="print-values-setup"}
A # calling the variable will display its value
print(A) # explicitly print the value of the variable
```
````

Students see only the exercise code, but `A <- 10` is available when
they run the exercise.

Use this pattern for any data, vectors, or variables that students need
inside an exercise but should not see as starter code.
