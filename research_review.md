<!--
Write a simple one page summary of the paper covering the following:

A brief summary of the paper's goals or techniques introduced (if any).
A brief summary of the paper's results (if any).
-->

# Research Review

"Mastering the game of Go with deep neural networks and tree search"
https://storage.googleapis.com/deepmind-media/alphago/AlphaGoNaturePaper.pdf

## Summary

### Techniques
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

They use *Value Networks* to evaluate board positions
and use *Policy Networks* to select moves.
And they skillfully combines:

1. __supervised learning__ (SL) from human expert games
  1. train policy network fast and efficient updates
  + also train a fast policy to be able to rapidly sample actions
1. __reinforcement learning__ (RL) from games of self-play
  1. train policy network by optimizing the final outcome of games
  + adjust the policy towards the correct goal of winning games
  + train value network to predicts the winner of games played by the
  RL policy network against itself

with Monte Carlo Tree Search (MCTS).

#### Supervised learning (SL) of policy networks

The SL policy network alternates between convolutional layers
with weights. The input to the policy network is simple representation
of the board state and a final outputs is a probability distribution
over all legal moves. The policy network is trained on randomly sampled state-action pairs,
using stochastic gradient ascent to maximize the likelihood of
the human move selected in state.

#### Reinforcement learning (RL) of policy networks

This training pipeline aims at improving the policy network by policy
gradient reinforcement learning.
They play games between the current policy network and
a randomly selected previous iteration of the policy network.
This randomize stabilizes training by preventing overfitting
to the current policy. They use a reward function that is zero
for all non-terminal time steps, and for terminal,
reward is from the perspective of the current player at each time step
+1 for winning and -1 for losing.
Then weights are updated at each time step by stochastic gradient ascent
 in the direction that maximizes expected outcome.

#### Reinforcement learning of valie networks

This stage focuses on position evaluation, estimating a value function
that predicts the outcome from position of games by using
same policy for both players.
They approximate the value function
with strongest policy (by RL policy network) using a value network
with weights.
The neural network has a similar architecture to the policy network,
but outputs a single prediction instead of a probability distribution.

#### Searching with policy and value networks
AlphaGo combines the policy and value networks in an MCTS algorithm,
that selects actions by lookahead search.
Each edge of the search tree stores an action value, visit count,
and prior probability. <!-- The tree is traversed by simulation
(that is, descending the tree in complete games without backup),
starting from the root state. At each time step of each simulation,
an action is selected from state so as to maximize action value
plus a bonus u similar to prior probability on visit count
that is proportional to the prior probability but devays with
repeated visits to encourage exploration.
When the traversal reaches a leaf node s_L at step L,
the leaf node may be expanded. The leaf position is proceeded
just once by the SL policy network. --> The output probabilities are
stored as prior probabilities for each legal action.
The leaf node is evaluated in two very different ways:
first, by the value network; and second, by the outcome of a
random rollout played out until terminal step using the fast rollout
policy; these evaluations are combined, using a mixing parameter lambda,
into a leaf evaluation.

### Results
- AlphaGo archieved a 99.8% winning rate against other Go programs
- Defeated the human European Go champion by 5 games to 0