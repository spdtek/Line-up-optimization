**Interested in contributing a code example?** 

Please take a look at our [contribution guidelines](CONTRIBUTING.md) before
getting started. Thanks!

<!-- Before submitting your code, please delete the above code contribution
instructions and this comment as they will not be relevant in your code 
example README.md.-->

# Line-up optimization

This demo, developed by Aitzol Iturrospe, uses the D-Wave Systems’ quantum annealer for optimizing the initial line-up of a soccer team.

Players and their playing position are selected to maximize the sum of players ratings in two different cases: a 4-3-3 attack formation and a 4-2-3-1 medium defensive formation. The problem is stated as a binary quadratic model (BQM) and it is solved in a D-Wave Leap’s Hybrid Solver.

Coach line-up decision making is of utmost importance for the performance of sport teams. One important decision that must be taken by a soccer coach is to determine the starting line-up of players. The coach considers many factors of each player and the team strategy, so it is a complex decision-making process (Saaty, 1994). The team formation describes how the players are positioned on the soccer field. Some players can play in more than one position, even if their valuation con be different for each position. The decision of the coach can impact team performance reducing their chances to win the match (Purwanto et al., 2018), e.g. if the appropriate players are not selected for a given formation or they are placed in positions where the cannot give their best.


Describe your example and specify what it is demonstrating. Consider the
following questions:

* Is it pedagogical or a usable application?
* Does it belong to a particular domain such as material simulation or logistics? 
* What level of Ocean proficiency does it target (beginner, advanced, pro)? 

A clear description allows us to properly categorize your example.

Images are encouraged. If your example produces a visualization, consider
displaying it here.

![D-Wave Logo](dwave_logo.png)

## Usage

A simple command that runs your program. For example,

```bash
python <demo_name>.py
```

If your example requires user input, make sure to specify any input limitations.

## Code Overview

A general overview of how the code works.

We prefer descriptions in bite-sized bullet points:

* Here's an example bullet point

## Code Specifics

Notable parts of the code implementation.

This is the place to:

* Highlight a part of the code implementation
* Talk about unusual or potentially difficult parts of the code
* Explain a code decision
* Explain how parameters were tuned

Note: there is no need to repeat everything that is already well-documented in
the code.

## References

A. Person, "Title of Amazing Information", [short link
name](https://example.com/)

## License

Released under the Apache License 2.0. See [LICENSE](LICENSE) file.
