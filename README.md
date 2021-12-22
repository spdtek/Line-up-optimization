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
The objective function to be maximized is the total sum of ratings of selected players, subject to the constraints in table 1, and the specific constraints for both formations considered in table 2 and table 3 respectively.

Maximize H<sub>Z</sub>=6.81x<sub>0</sub>+5.86x<sub>1</sub>+6.62x<sub>2</sub>+⋯+6.03x<sub>40</sub>+8.22x<sub>41</sub>+5.84x<sub>42</sub>

## Usage

To run the demo, type:

python lineup_optim.py

The user will be prompted for the formation to be optimized: 1 (default) for a 4-3-3 formation or 2 for a 4-3-2-1 formation.
After running the optimization, output will be printed to the command line that showing the optimized line-up for the choosen formation and total rating. 

Binary variable  | Player Name  | Position  | Rating
------------- | ------------- | ------------- | -------------
x<sub>1</sub> | Alisson | GK | 6.81
x<sub>6</sub> | Philips | DC | 7.24
x<sub>7</sub> | Fabinho | DC | 7.11 
x<sub>8</sub> | Robertson | DL | 6.85
x<sub>11</sub> | Milner | DR | 8.15 
x<sub>18</sub> | Williams | CM | 7.77 
x<sub>21</sub> | Thiago | CM | 7.38 
x<sub>28</sub> | Jota | CM | 9.39
x<sub>34</sub> | Mane | FWL | 7.56
x<sub>37</sub> | Salah | FWR | 7.42 
x<sub>39</sub> | Firminho | FW | 6.99 
 |  |  | Max H<sub>Z</sub> | 82.67

In addition, the list of constraints will be visualized showing wether if they are fulfilled (true) o not (false).


## Code Overview

Equality constraints <img src="image027.png" style="vertical-align: -100px; margin: 0;" width=8% height=8%> are standardly formulated in BQMs as minimizing <img src="image028.png" style="vertical-align: -100px; margin: 0;" width=10% height=10%> functions. Therefore, the constraints are formulated following the quadratic formulation and they are shown in tables 1, 2 and 3.

Table.1 - General constraints

Constraint  | Explanation  | Nomenclature
------------- | ------------- | -------------
(x<sub>0</sub>+x<sub>1</sub>+x<sub>2</sub>+⋯+x<sub>40</sub>+x<sub>41</sub>+x<sub>42</sub>-11)<sup>2</sup>  | 11 players  | C<sub>1</sub>
(x<sub>0</sub>+x<sub>1</sub>-1)<sup>2</sup>  | 1 goalkeeper  | C<sub>2</sub>
(x<sub>2</sub>+x<sub>3</sub>+x<sub>4</sub>+x<sub>5</sub>+x<sub>6</sub>-2)<sup>2</sup>  | 2 central defenders  | C<sub>3</sub>
(x<sub>7</sub>-1)<sup>1</sup>  | 1 left-hand side defender  | C<sub>4</sub>
(x<sub>8</sub>+x<sub>9</sub>+x<sub>10</sub>-1)<sup>2</sup>  | 1 right-hand side defender  | C<sub>5</sub>
(x<sub>38</sub>+x<sub>39</sub>+x<sub>40</sub>+x<sub>41</sub>+x<sub>42</sub>-1)<sup>2</sup>  | 1 forward/striker  | C<sub>6</sub>

Table.2 - Constraints for formation 4-3-3

Constraint  | Explanation  | Nomenclature
------------- | ------------- | -------------
(x<sub>16</sub>+x<sub>17</sub>+x<sub>18</sub>+⋯+x<sub>25</sub>+x<sub>26</sub>+x<sub>27</sub>-3)<sup>2</sup>  | 3 central midfielders  | C<sub>7</sub>
(x<sub>33</sub>+x<sub>34</sub>+x<sub>35</sub>-1)<sup>2</sup>  | 1 left forward  | C<sub>8</sub>
(x<sub>36</sub>+x<sub>37</sub>-1)<sup>2</sup>  | 1 right forward  | C<sub>9</sub>

Table.3 - Constraints for formation 4-3-2-1

Constraint  | Explanation  | Nomenclature
------------- | ------------- | -------------
(x<sub>11</sub>+x<sub>12</sub>+x<sub>13</sub>+x<sub>14</sub>+x<sub>15</sub>-2)<sup>2</sup>  | 2 defensive midfielders  | C<sub>10</sub>
(x<sub>28</sub>+x<sub>29</sub>+x<sub>30</sub>+x<sub>31</sub>+x<sub>32</sub>-3)<sup>2</sup>  | 3 attacking midfielder  | C<sub>11</sub>

For both formations, we impose the following inequalities as constraints to avoid solutions with players in multiple positions. For inequality constraints, slack variables are introduced in order to reduce them to equalities (DWAVE, 2021) (as shown in table 4).

Table 4. Constraints to avoid solutions with the same player in different positions

Constraint  | Nomenclature
------------- | -------------
(x<sub>7</sub>+x<sub>11</sub>+x<sub>16</sub>+a<sub>0</sub>-1)<sup>2</sup>  | I<sub>1</sub>
(x<sub>8</sub>+x<sub>12</sub>+a<sub>1</sub>-1)<sup>2</sup>  | I<sub>2</sub>
(x<sub>9</sub>+x<sub>13</sub>+x<sub>17</sub>+a<sub>2</sub>-1)<sup>2</sup>  | I<sub>3</sub>
(x<sub>14</sub>+x<sub>19</sub>+x<sub>28</sub>+a<sub>3</sub>-1)<sup>2</sup>  | I<sub>4</sub>
(x<sub>10</sub>+x<sub>21</sub>+a<sub>4</sub>-1)<sup>2</sup>  | I<sub>5</sub>
(x<sub>15</sub>+x<sub>23</sub>+a<sub>5</sub>-1)<sup>2</sup>  | I<sub>6</sub>
(x<sub>25</sub>+x<sub>29</sub>+a<sub>6</sub>-1)<sup>2</sup>  | I<sub>7</sub>
(x<sub>31</sub>+x<sub>33</sub>+a<sub>7</sub>-1)<sup>2</sup>  | I<sub>8</sub>
(x<sub>36</sub>+x<sub>39</sub>+a<sub>8</sub>-1)<sup>2</sup>  | I<sub>9</sub>
(x<sub>27</sub>+x<sub>32</sub>+x<sub>34</sub>+x<sub>37</sub>+x<sub>41</sub>+a<sub>9</sub>-1)<sup>2</sup>  | I<sub>10</sub>

The Lagrange multiplier (λ<sub>i</sub>) acts as a weight given to the constraint. It should be set high enough to ensure the constraint is satisfied but setting it too high obscures the real function we are trying to minimize. All the Lagrange multipliers were set equal to each other and further equal to eleven times the maximum rating.

As the objective function is a maximization function, it is converted to a minimization by multiplying the H<sub>Z</sub> expression by -1.

H<sub>433</sub> = -H<sub>Z</sub> + λ(C<sub>1</sub>+C<sub>2</sub>+C<sub>3</sub>+C<sub>4</sub>+C<sub>5</sub>+C<sub>6</sub>+C<sub>7</sub>+C<sub>8</sub>+C<sub>9</sub>+I<sub>1</sub>+I<sub>2</sub>+I<sub>3</sub>+I<sub>4</sub>+I<sub>5</sub>+I<sub>6</sub>+I<sub>7</sub>+I<sub>8</sub>+I<sub>9</sub>+I<sub>10</sub>)

H<sub>4321</sub> = -H<sub>Z</sub> + λ(C<sub>1</sub>+C<sub>2</sub>+C<sub>3</sub>+C<sub>4</sub>+C<sub>5</sub>+C<sub>6</sub>+C<sub>10</sub>+C<sub>11</sub>+I<sub>1</sub>+I<sub>2</sub>+I<sub>3</sub>+I<sub>4</sub>+I<sub>5</sub>+I<sub>6</sub>+I<sub>7</sub>+I<sub>8</sub>+I<sub>9</sub>+I<sub>10</sub>)

## References

(DWAVE, 2021) D-wave problem-solving handbook. https://docs.dwavesys.com/docs/latest/doc_handbook.html. Accessed 18 Dec 2021.
(Mahrudinda et al., 2020) Mahrudinda, Sudrajat Supian, S. Subiyanto and Chaerani, D.  Optimization of The Best Line-up in Football using Binary Integer Programming Model. International Journal of Global Operations Research, Vol. 1, No. 3, pp. 114-122, 2020.


## License

Released under the Apache License 2.0. See [LICENSE](LICENSE) file.
