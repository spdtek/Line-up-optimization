**Interested in contributing a code example?** 

# Line-up optimization

The aim of this demo, developed by Aitzol Iturrospe, is to optimize the initial line-up of a soccer team. The goal is to select players maximizing the sum of their ratings. Two different cases are considered: 
 - a 4-3-3 attack formation and 
 - a 4-2-3-1 medium defensive formation. 

The problem is stated as a binary quadratic model (BQM) and it is solved in a D-Wave Leap’s Hybrid Solver.

The eleven football players are divided into several positions in accordance with the team formation. In addition to one goalkeeper (GK), the players are divided into three main positions, defenders (D), midfielders (M), and forward/strikers (FW). Each major position can be subdivided into several more specific positions, e.g. for the defender is divided into central defender (DC), left wing defender (DL) and right wing defender (DR). The midfielder's position can be divided into defensive midfielder (DM), central midfielder (CM) and attack midfielder (AM). The forward’s positions might be divided into right wing forward (FWR), left wing forward (FWL) and forward (FW). Figure 1 shows players’ ratings depending on the position as presented in the article (Mahrudinda et al., 2020). Each pair (player, position) will be considered a binary variable; being 1 if the player is lined up to play in that position and 0 otherwise.

![D-Wave Logo](dwave_logo.png)








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
