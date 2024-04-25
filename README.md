
# Knapsack Solvers Source Code Survey

[![build](../../actions/workflows/build.yml/badge.svg)](../../actions/)
![Platforms: Linux, MacOS, Windows](https://img.shields.io/badge/Platform-Linux%20%7C%20MacOS%20%7C%20Windows-blue.svg)
[![Language: Python](https://img.shields.io/badge/Language-Python-blue.svg)](https://www.python.org/)
[![Code Style: Black](https://img.shields.io/badge/Code%20Style-Black-blue.svg)](https://github.com/psf/black)
[![Commits: Conventional](https://img.shields.io/badge/Commits-Conventional-blue.svg)](https://www.conventionalcommits.org/en/v1.0.0/)
[![Discord](https://img.shields.io/discord/872320492936257537?logo=discord)](https://discord.gg/kjah8MFYbR)

## Introduction

- Due date: Check Discord or the
  [Course Materials Schedule](https://github.com/allegheny-college-cmpsc-101-spring-2024/course-materials/blob/main/Schedule.md)
- This assignment is graded as
  described in the syllabus section for a Programming Project
  [Assignment Evaluation](https://github.com/allegheny-college-cmpsc-101-spring-2024/course-materials?tab=readme-ov-file#assignment-evaluation)
- Submit this assignment on GitHub following the expectations in the syllabus on
  [Assignment Submission](https://github.com/allegheny-college-cmpsc-101-spring-2024/course-materials#assignment-submission).
- To begin, read this `README`
- This project has been adapted from
  [Proactive Programmers' material](https://proactiveprogrammers.com/data-abstraction/source-code-surveys/knapsack-solvers/),
  thus discrepancies are possible.
- Post to the #data-structures Discord channel for questions and clarifications.
- For reference, check the
  [starter repo](https://github.com/allegheny-college-cmpsc-101-spring-2024/knapsack-solvers-starter)
- Modifications to the gatorgrade.yml file are not permitted without explicit instruction.

## Learning Objectives

The learning objectives of this assignment are to:

1. Use Git and GitHub to manage source code file changes
2. Use abstract data types
3. Define higher-order functions
4. Run greedy and exhaustive optimization algorithms
5. Write clearly about the programming concepts in this assignment.

## Seeking Assistance

Please review the course expectations on the syllabus about
[Seeking Assistance](https://github.com/allegheny-college-cmpsc-101-spring-2024/course-materials#seeking-assistance).
Students are reminded to uphold the Honor Code. Cloning the assignment repository is a
commitment to the latter.

For this assignment, you may use class materials, textbooks, notes, and the
internet. Ensure that your writing is original and based on your own understanding
of the concepts.

To claim that work is your own, it is essential to craft the logic and the
writing together without copying or using the logical structure of another
source. The honor code holds everyone to this standard.

If outside of lab you have questions, the #data-structures Discord channel,
TL office hours, instructor office hours, and GitHub Issues can be utilized.

## Project Goals ([Project Overview](#project-overview) Below)

This assignment invites you to study, repair, and test a Python programs called
`demonstrate-knapsack-solvers`. The 0/1 Knapsack problem requires a computer
program to determine which items to pick, from a list of items with both costs
and benefits, in order to maximize the benefits while ensuring that the costs do
not exceed a specified maximum cost. As part of this source code survey you will
will implement and run three different greedy solvers called
`greedy-by-density`, `greedy-by-weight`, and `greedy-by-value` that vary in the
way in which they select items. You will also implement and run an exhaustive
0/1 knapsack solver that is guaranteed to find the optimal solution for a
specific problem instance. With that said, this exhaustive solver must generate
the powerset of the set of all items and is thus only efficient for small
knapsack instances. After running all three of the greedy solvers and then
exhaustive solver you will be able to determine which greedy approach is best
suited for the problem instance.

## Code Survey

If you change into the `source/` directory of your GitHub repository, you will
see one Python file called `demonstrate-knapsack-solvers.py`. The
`demonstrate-knapsack-solvers` module contains an incomplete class definition
written as `class Item(object):`. You need to follow the `TODO` markers in this
class definition, by inputting the source code from the text book, for functions
like the constructor `def __init__(self, n, v, w)` and like accessor functions
such as `def get_name(self) -> str`, `def get_value(self) -> int`, `def
get_weight(self) -> int`. Since your textbook does not provide an implementation
of a function for generating the powerset of a set, you will also need to
consult the references in the source code or create your own function. Finally,
you will need to implement the function that uses the generated powerset to
perform an exhaustive search of all possible combinations of input.

To ensure that the `demonstrate-knapsack-solvers.py` script analyzes the same
instance of the 0/1 knapsack problem as is found in the textbook, you should use
the following `build_items` function that is also available in the provided
source code. Lines `3` through `5` of this function respectively create the
input to the knapsack solver that includes the name of the item and its value
and weight (i.e., its cost). Lines `6` through `8` of this function populate the
`items` `List` with all of the previously created instances of `Item`. Finally,
the `List` of `Item` objects returned by this function on line `9` will be
processed by both the greedy and exhaustive solvers.

```python linenums="1"
def build_items() -> List[Item]:
    """Create an instance of a 0/1 knapsack using instances of Item."""
    names = ["Clock", "Painting", "Radio", "Vase", "Book", "Computer"]
    values = [175, 90, 20, 50, 10, 200]
    weights = [10, 9, 4, 2, 1, 20]
    items: List[Item] = []
    for i in range(len(values)):
        items.append(Item(names[i], values[i], weights[i]))
    return items
```

After you have addressed all of the `TODO` markers inside of the provided source
code, you can run the program by typing the command `python
demonstrate-knapsack-solvers.py` as long as you have changed into the `source/`
directory. If you correctly implemented the program and provided all of the
source code required by the `TODO` markers it should produce the following
output. It is important to note that, at least for this instance of the 0/1
knapsack problem, the `greedy-by-density` greedy solver produces the solution
that is closest to the optimal one given by the exhaustive solver. Why do you
think that this greedy solver produced the best solution? Do you think that it
is always going to yield the best solution? Why or why not?

```text
Running all of the knapsack solvers!

Using greedy-by-value to fill knapsack of size 20
Total value of items taken is 200.0
   (Computer, 200, 20)

Using greedy-by-weight to fill knapsack of size 20
Total value of items taken is 170.0
   (Book, 10, 1)
   (Vase, 50, 2)
   (Radio, 20, 4)
   (Painting, 90, 9)

Using greedy-by-density to fill knapsack of size 20
Total value of items taken is 255.0
   (Vase, 50, 2)
   (Clock, 175, 10)
   (Book, 10, 1)
   (Radio, 20, 4)

Generating the powerset of all items!

Using exhaustive enumeration to fill a knapsack of size 20
Total value of items taken is 275.0
   (Clock, 175, 10)
   (Painting, 90, 9)
   (Book, 10, 1)
```

## Running Checks

Since this project does not use [Poetry](https://python-poetry.org/) to manage
project dependencies and virtual environments, it does not support the use of
commands like `poetry run task test`. However, you can leverage the relevant
instructions in the [technical
skills](/proactive-skills/introduction-proactive-skills/) to run the command
`gatorgrade --config config/gatorgrade.yml` to check your work. If your work
meets the baseline requirements and adheres to the best practices that proactive
programmers adopt you will see that all the checks pass when you run
`gatorgrade`. You can study the `config/gatorgrade.yml` file in your repository
to learn how :material-github:
[GatorGrade](https://github.com/GatorEducator/gatorgrade) runs :material-github:
[GatorGrader](https://github.com/GatorEducator/gatorgrader) to automatically
check your program and technical writing.

## Project Reflection

Once you have finished all of the previous technical tasks, you can use a text
editor to answer all of the questions in the `writing/reflection.md` file. Since
this is a source code survey, you should provide output from running each of the
provided Python programs on your own laptop and then explain how the program's
source code produced that output. A specific goal for this project is to ensure
that you can explain the behavior of the greedy solvers called
`greedy-by-density`, `greedy-by-weight`, and `greedy-by-value`. You should also
be able to explain the trade-offs in terms of solution quality and efficiency of
the knapsack solver that uses the exhaustive enumeration strategy.

## Project Assessment

Since this project is source code survey, it is aligned with the **remembering**
and **understanding** levels of [Bloom's
taxonomy](/proactive-learning/blooms-taxonomy/). You can learn more about how a
proactive programming expert will assess your work by examining the [assessment
strategy](/proactive-learning/assessment-strategy/). From the start to the end
of this project you may make an unlimited number of reattempts at submitting
source code and technical writing that meet the project's specification.

## Project Overview

After cloning this repository to your computer, please take the following steps:

- Use the `cd` command to change into the directory for this repository.
- Change into the program source code directory by typing `cd source`.
- Run both of the provided Python scripts by typing the following:
  - `python demonstrate_knapsack_solvers.py`: demonstrate use of knapsack solvers
- Confirm that the programs are producing the expected output.
- You may refer to the course textbook, slides, and Colab notes.
- Make sure that you can explain why the programs produce the output that they do.
- run the automated grading checks by typing
  `gatorgrade --config config/gatorgrade.yml`.
- You may also review the output from running GatorGrader in GitHub Actions.
- Don't forget to provide all of the required responses to the technical writing
  prompts in the `writing/reflection.md` file.
- Please make sure that you completely delete the `TODO` markers and their
  labels from all of the provided source code.
- Please make sure that you also completely delete the `TODO` markers and their
  labels from every line of the `writing/reflection.md` file.
