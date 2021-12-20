**Interested in contributing a code example?** 
<table style="max-width: 100%;"><tbody><tr>
# Line-up optimization

The aim of this demo, developed by Aitzol Iturrospe, is to optimize the initial line-up of Liverpool FC. The goal is to select players
maximizing the sum of their ratings. Two different cases are considered: 
 - a 4-3-3 attack formation and 
 - a 4-2-3-1 medium defensive formation. 

The problem is stated as a binary quadratic model (BQM) and it is solved in a D-Wave Leap’s Hybrid Solver.

The eleven football players are divided into several positions in accordance with the team formation. In addition to one goalkeeper
(GK), the players are divided into three main positions, defenders (D), midfielders (M), and forward/strikers (FW). Each major position
can be subdivided into several more specific positions, such as
- central defender (DC),
- left wing defender (DL),
- right wing defender (DR),
- defensive midfielder (DM), 
- central midfielder (CM),
- attack midfielder (AM),
- right wing forward (FWR),
- left wing forward (FWL) or
- forward/striker (FW)

Figure 1 shows Liverpool FC football players’ ratings depending on the position as presented in the article (Mahrudinda et al., 2020) in
the English Premier League during the 2020/2021 season. Each pair (player, position) will be considered as a binary variable; being 1 if
the player is lined up to play in that position and 0 otherwise.


<p align="center" dir="auto">
</p><p dir="auto"><img src="ratings.png" alt="Figure 1" title="Players’ ratings" style="max-width: 100%;"></p>
<p dir="auto">
Fig.1 - Players’ ratings (Mahrudinda et al., 2020).
</p>


Constraint  | Explanation  | Nomenclature
------------- | ------------- | -------------
(x<sub>1</sub>+x<sub>2</sub>+x<sub>3</sub>+⋯+x<sub>41</sub>+x<sub>42</sub>+x<sub>43</sub>-11)<sup>2</sup>  | 11 players  | C<sub>1</sub>
(x<sub>1</sub>+x<sub>2</sub>-1)<sup>2</sup>  | 1 goalkeeper  | C<sub>2</sub>
(x<sub>3</sub>+x<sub>4</sub>+x<sub>5</sub>+x<sub>6</sub>+x<sub>7</sub>-2)<sup>2</sup>  | 2 central defenders  | C<sub>3</sub>
(x<sub>8</sub>-1)<sup>2</sup>  | 1 left-hand side defender  | C<sub>4</sub>
(x<sub>9</sub>+x<sub>10</sub>+x<sub>11</sub>-1)<sup>2</sup>  | 1 right-hand side defender  | C<sub>5</sub>
(x<sub>39</sub>+x<sub>40</sub>+x<sub>41</sub>+x<sub>42</sub>+x<sub>43</sub>-1)<sup>2</sup>  | 1 forward/striker  | C<sub>6</sub>

Constraint  | Explanation  | Nomenclature
------------- | ------------- | -------------
(x<sub>17</sub>+x<sub>18</sub>+x<sub>19</sub>+⋯+x<sub>26</sub>+x<sub>27</sub>+x<sub>28</sub>-3)<sup>2</sup>  | 3 central midfielders  | C<sub>7</sub>
(x<sub>34</sub>+x<sub>35</sub>+x<sub>36</sub>-1)<sup>2</sup>  | 1 left forward  | C<sub>8</sub>
(x<sub>37</sub>+x<sub>38</sub>-1)<sup>2</sup>  | 1 right forward  | C<sub>9</sub>


Constraint  | Explanation  | Nomenclature
------------- | ------------- | -------------
(x<sub>12</sub>+x<sub>13</sub>+x<sub>14</sub>+x<sub>15</sub>+x<sub>16</sub>-2)<sup>2</sup>  | 2 defensive midfielders  | C<sub>10</sub>
(x<sub>29</sub>+x<sub>30</sub>+x<sub>31</sub>+x<sub>32</sub>+x<sub>33</sub>-3)<sup>2</sup>  | 3 attacking midfielder  | C<sub>11</sub>


QPU results for 4-3-3 formation 	Results for 4-3-3 formation in (Mahrudinda et al., 2020)

Binary variable  | Player Name  | Position  | Rating  | Binary variable  | Player Name  | Position  | Rating
------------- | ------------- | ------------- | ------------- | ------------- | ------------- | ------------- | -------------
x<sub>1</sub> | Alisson | GK | 6.81 | x<sub>1</sub> | Alisson | GK | 6.81 
x<sub>6</sub> | Philips | DC | 7.24 | x<sub>4</sub> | Gomez | DC | 6.91 
x<sub>7</sub> | Fabinho | DC | 7.11 | x<sub>6</sub> | Philips | DC | 7.24 
x<sub>8</sub> | Robertson | DL | 6.85 | x<sub>8</sub> | Robertson | DL | 6.85 
x<sub>11</sub> | Milner | DR | 8.15 | x<sub>11</sub> | Milner | DR | 8.15 
x<sub>18</sub> | Williams | CM | 7.77 | x<sub>18</sub> | Williams | CM | 7.77 
x<sub>21</sub> | Thiago | CM | 7.38 | x<sub>21</sub> | Thiago | CM | 7.38 
x<sub>28</sub> | Jota | CM | 9.39 | x<sub>28</sub> | Jota | CM | 9.39 
x<sub>34</sub> | Mane | FWL | 7.56 | x<sub>34</sub> | Mane | FWL | 7.56 
x<sub>37</sub> | Salah | FWR | 7.42 | x<sub>37</sub> | Salah | FWR | 7.42 
x<sub>39</sub> | Firminho | FW | 6.99 | x<sub>39</sub> | Firminho | FW | 6.99 
 |  |  | Max H<sub>Z</sub> | 82.67 |  |  |  	Max H<sub>Z</sub> | 82.47


Binary variable  | Player Name  | Position  | Rating  | Binary variable  | Player Name  | Position  | Rating
------------- | ------------- | ------------- | ------------- | ------------- | ------------- | ------------- | -------------
x<sub>1</sub> | Alisson | GK | 6.81 | x<sub>1</sub> | Alisson | GK | 6.81 
x<sub>6</sub> | Philips | DC | 7.24 | x<sub>6</sub> | Gomez | DC | 6.91 
x<sub>7</sub> | Fabinho | DC | 7.11 | x<sub>7</sub> | Philips | DC | 7.24 
x<sub>8</sub> | Robertson | DL | 6.85 | x<sub>8</sub> | Robertson | DL | 6.85 
x<sub>11</sub> | Milner | DR | 8.15 | x<sub>11</sub> | Milner | DR | 8.15 
x<sub>14</sub> | Williams | DM | 7.66 | x<sub>14</sub> | Williams | DM | 7.66 
x<sub>16</sub> | Henderson | DM | 6.80 | x<sub>16</sub> | Henderson | DM | 6.80 
x<sub>29</sub> | Wijnaldum | AM | 7.16 | x<sub>29</sub> | Wijnaldum | AM | 7.16
x<sub>31</sub> | Firminho | AM | 6.80 | x<sub>31</sub> | Firminho | AM | 6.80
x<sub>32</sub> | Mane | AM | 7.24 | x<sub>32</sub> | Mane | AM | 7.24 
x<sub>42</sub> | Jota | FW | 8.22 | x<sub>42</sub> | Jota | FW | 8.22
 |  |  | Max H<sub>Z</sub> | 80.04 |  |  |  	Max H<sub>Z</sub> | 80.04













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
