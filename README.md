ISAAK's R Style Guide
======================

R is a high-level programming language used primarily for statistical
computing and graphics. The goal of the R Programming Style Guide is to
make our R code easier to read, share, and verify. The rules below were
designed after Google's R Style Guide.

Summary: R Style Rules
----------------------

1.  [File Names](#file-names): end in `.R`
2.  [Identifiers](#identifiers): `variable_name_type`, `function_name`, `CONSTANTNAME`
3.  [Line Length](#line-length): maximum 80 characters
4.  [Indentation](#indentation): two spaces, no tabs
5.  [Spacing](#spacing)
6.  [Curly Braces](#curly-braces): first on same line, last on own line
7.  [else](#else): Surround else with braces
8.  [Assignment](#assignment): use `<-`, not `=`
9.  [Semicolons](#semicolons): don't use them
10. [General Layout and Ordering](#general-layout-and-ordering)
11. [Commenting Guidelines](#commenting-guidelines): all comments begin with `#`
    followed by a space; inline comments need two spaces before the `#`
12. [Function Definitions and Calls](#function-definitions-and-calls)
13. [Function Documentation](#function-documentation)
14. [Example Function](#example-function)
15. [TODO Style](#todo-style): `TODO(username)`

Summary: R Language Rules
-------------------------

1.  [`attach`](#attach): avoid using it
2.  [Functions](#functions): errors should be raised using
    `stop()`
3.  [Objects and Methods](#objects-and-methods): avoid S4 objects and methods when
    possible; never mix S3 and S4

### Notation and Naming

#### File Names

File names should end in `.R` and, of course, be meaningful.\
GOOD: `predict_ad_revenue.R`\
BAD: `foo.R`

#### Identifiers

Use underscores ( `_` ) but no hyphens ( `-` ) in identifiers.
Identifiers should be named according to the following conventions. The
preferred form for variable names is all lower case letters and words
separated with underscores. The variable names have suffixes identifying the data type according to the list below  (`variable_name_s`); Function names have lower case letters separated by underscores (`function_name`); constants are named in all caps `CONSTANT_NAME`.

-   `variable_name_type` is good\
    OK: `avg_clicks_s`\
		Make variable name noun.\
-   `function_name`\
    GOOD: `calculate_avg_clicks`\
    Make function names verbs.\
    *Exception: When creating a classed object, the function
    name (constructor) and class should match (e.g., lm).*
-   `CONSTANTNAME`


#### Suffix
- nu numeric
- ch character
- df dataframe
- ma matrix
- ti tibble
- bo boolean
- fa factor
- li list

### Syntax

#### Line Length

The maximum line length is 80 characters.

#### Indentation

When indenting your code, use tabs. Try to avoid mixing spaces and tabs.
*Exception: When a line break occurs inside parentheses, align the
wrapped line with the first character inside the parenthesis.*

#### Spacing

Place spaces around all binary operators (`=`, `+`, `-`, `<-`, etc.).\

Do not place a space before a comma, but always place one after a
comma.\
\
GOOD:

    tab_prior_df <- table(df[df$days_from_opt < 0, "campaign_id"])
    total_nu <- sum(x_df[, 1])
    total_nu <- sum(x_df[1, ])


Place a space before left parenthesis, except in a function call.

GOOD:\
`if (debug)`

Extra spacing (i.e., more than one space in a row) is okay if it
improves alignment of equals signs or arrows (`<-`).

    plot(x    = x_coord_nu,
         y    = data_ma[, 1],
         ylim = ylim_nu,
         xlab = "dates",
         ylab = metric_ch,
         main = (paste(metric_ch, " for 3 samples ", sep = "")))

Do not place spaces around code in parentheses or square brackets.\
*Exception: Always place a space after a comma.*

GOOD:

    if (debug_bo)
    x_df[1, ]


#### Curly Braces

An opening curly brace should never go on its own line; a closing curly
brace should always go on its own line. You may not omit curly braces when a
block consists of a single statement.

    if (is.null(ylim_nu)) {
      ylim_nu <- c(0, 0.06)
    }

Always begin the body of a block on a new line.

BAD:\
` if (is.null(ylim))               ylim <- c(0, 0.06)`\
` if (is.null(ylim))               {ylim <- c(0, 0.06)} `

#### Surround else with braces

An `else` statement should always be surrounded on the same line by
curly braces.

    if (condition) {
      one or more lines
    } else {
      one or more lines
    }

#### Assignment

Use `<-`, not `=`, for assignment.

GOOD:\
` x <- 5 `

#### Semicolons

Do not terminate your lines with semicolons or use semicolons to put
more than one command on the same line. Semicolons are not necessary.

### Organization

#### General Layout and Ordering

If everyone uses the same general ordering, we'll be able to read and
understand each other's scripts faster and more easily.

1.  Copyright statement comment
2.  Author comment
3.  File description comment, including purpose of program, inputs, and
    outputs
4.  `source()` and `library()` statements
5.  Function definitions
6.  Executed statements, if applicable (e.g., ` print`, `plot`)

Unit tests should go in a separate file named `test_originalfilename.R`.

#### Commenting Guidelines

Comment your code. Entire commented lines should begin with `#` and one
space.

Short comments can be placed after code preceded by two spaces, `#`, and
then one space.

    # Create histogram of frequency of campaigns by pct budget spent.
    hist(example_df$pct_spent,
         breaks = "scott",  # method for choosing number of buckets
         main   = "Histogram: fraction budget spent by campaignid",
         xlab   = "Fraction of budget spent",
         ylab   = "Frequency (count of campaignids)")

#### Function Definitions and Calls

Function definitions should first list arguments without default values,
followed by those with default values.

In both function definitions and function calls, multiple arguments per
line are allowed; line breaks are only allowed between assignments.\
GOOD:

    PredictCTR <- function(query_ch, property_bo, num_days_nu,
                           show_plot = TRUE)


Ideally, unit tests should serve as sample function calls (for shared
library routines).

#### Function Documentation

Please follow the guidelines of roxygen2 (https://github.com/klutometis/roxygen).

#### TODO Style

Use a consistent style for TODOs throughout your code.\
`# TODO(username): Explicit description of action to be taken`

### Language

#### Attach

The possibilities for creating errors when using `attach` are numerous.
Avoid it.

#### Functions

Errors should be raised using `stop()`.

#### Objects and Methods

The S language has two object systems, S3 and S4, both of which are
available in R. S3 methods are more interactive and flexible, whereas S4
methods are more formal and rigorous. (For an illustration of the two
systems, see Thomas Lumley's "Programmer's Niche: A Simple Class, in S3
and S4" in R News 4/1, 2004, pgs. 33 - 36:
<https://cran.r-project.org/doc/Rnews/Rnews_2004-1.pdf>.)

Use S3 objects and methods unless there is a strong reason to use S4
objects or methods. A primary justification for an S4 object would be to
use objects directly in C++ code. A primary justification for an S4
generic/method would be to dispatch on two arguments.

Avoid mixing S3 and S4: S4 methods ignore S3 inheritance and vice-versa.

### Exceptions

The coding conventions described above should be followed, unless there
is good reason to do otherwise. Exceptions include legacy code and
modifying third-party code.


### References

- Template: [Google R Style Guide](https://google.github.io/styleguide/Rguide.xml)
- [R Style. An Rchaeological Commentary.](https://cran.r-project.org/web/packages/rockchalk/vignettes/Rstyle.pdf)
- [Wickham's Advanced R Style Guide](http://adv-r.had.co.nz/Style.html)
- [Yihui Xie's formatR](https://yihui.name/formatr/)

