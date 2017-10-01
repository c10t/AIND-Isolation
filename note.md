<!-- playing matches with custom_score and custom_score_2 switched
                        *************************
                             Playing Matches
                        *************************

 Match #   Opponent    AB_Improved   AB_Custom   AB_Custom_2  AB_Custom_3
                        Won | Lost   Won | Lost   Won | Lost   Won | Lost
    1       Random       8  |   2     8  |   2     6  |   4     9  |   1
    2       MM_Open      8  |   2     7  |   3     6  |   4     6  |   4
    3      MM_Center     6  |   4     9  |   1    10  |   0     7  |   3
    4     MM_Improved    5  |   5     6  |   4     6  |   4     5  |   5
    5       AB_Open      5  |   5     6  |   4     6  |   4     3  |   7
    6      AB_Center     5  |   5     6  |   4     8  |   2     5  |   5
    7     AB_Improved    6  |   4     3  |   7     5  |   5     5  |   5
--------------------------------------------------------------------------
           Win Rate:      61.4%        64.3%        67.1%        57.1%
-->

<!--
Write a simple one page summary of the paper covering the following:

A brief summary of the paper's goals or techniques introduced (if any).
A brief summary of the paper's results (if any).
-->

<!-- - use *Value Networks* to evaluate board positions
- use *Policy Networks* to select moves
- a novel combination of supervised learning from human expert games
and reinforcement learning from games of self-play
- combines Monte Carlo simulation with value and policy networks
- the strongest current Go programs are based on MCTS (Monte Carlo
Tree Search),
enhanced by policies that are trained to predict human expert moves
- these policies are used to narrow the search
to beam of high-probability actions,
and to sample actions during rollouts
- this approach has archieved strong amateur play
- However, prior work has been limited to shallow policies or
value functions based on a linear combination of input features
- Recently, deep convolutional neural networks have archieved
unprecedented performance in visual domains

- they use many layers of newrons, each arranged in overlapping tiles,
to construct increasingly abstract, localized representations
- employ a similar architecture for the game of Go
- pass in the board position as a 19 x 19 image

- __use conv. layers__ to construct a representation of the position
- use these neural networks __to reduce the effective depth__ and
__breadth of the search tree__:
evaluating positions using a value network, and
sampling actions using a policy network

- train a the neural networks using a pipeline
consisting of several stages of machine learning

- begin by training a supervised leaning (SL) policy network p_sigma
directly from expert human moves
- -> this provides fast, efficient learning updates
with immediate feedback and high-quality gradients
- Similar to prior work 13, 15, we also train a fast policy p_pi
that can rapidly sample actions during rollouts
- next, train a reinforcement learning (RL) policy network p_rho
that improves the SL policy network by optimizing the final outcome of
games of self-play
- this adjusts the policy towards the correct goal of winning games,
rather than maximizing predictive accuracy
- finally train a value network nu_theta that predicts the winner of
games played by the RL policy network against itsekf
- Their program AlphaGo efficiently __combines the policy and value
networks with MCTS__ -->

<!-- The tree is traversed by simulation
(that is, descending the tree in complete games without backup),
starting from the root state. At each time step of each simulation,
an action is selected from state so as to maximize action value
plus a bonus u similar to prior probability on visit count
that is proportional to the prior probability but devays with
repeated visits to encourage exploration.
When the traversal reaches a leaf node s_L at step L,
the leaf node may be expanded. The leaf position is proceeded
just once by the SL policy network. -->