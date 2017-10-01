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

# Heuristic Analysys

## custom_score_2()
This function evaluates each action by subtract inactive player's
legal moves from active player's legal moves.
Each count of moves are squared to emphasis the difference.
This function based on the simple consideration:
The more action able to choice, the harder to be checkmated.


| Opponent    | Won | Lost |
| ----------- | --- | ---- |
| Random      | 8   | 2    |
| MM_Open     | 7   | 3    |
| MM_Center   | 9   | 1    |
| MM_Improved | 6   | 4    |
| AB_Open     | 6   | 4    |
| AB_Center   | 6   | 4    |
| AB_Improved | 3   | 7    |
__*Win Rate: 64.3%*__

This rate is not bad, but this function seems difficult
 to defeat AB_Improved.

## custom_score()
This function evaluates each action by ratio of inactive player's
legal moves and active player's legal moves.


| Opponent    | Won | Lost |
| ----------- | --- | ---- |
| Random      | 6   | 4    |
| MM_Open     | 6   | 4    |
| MM_Center   | 10  | 0    |
| MM_Improved | 6   | 4    |
| AB_Open     | 6   | 4    |
| AB_Center   | 8   | 2    |
| AB_Improved | 5   | 5    |
__*Win Rate: 67.1%*__

Win rate is improved from __custom_score()__ instead of
decreasing wins against *Random* and *MM_Open* opponent.
Especially this becomes getting even score against *AB_Improved*.

## custom_score_3()
This function evaluates each action by the distance between
each player's location. This function based on the consideration
that it is good at keeping long distance in order to be alive.


| Opponent    | Won | Lost |
| ----------- | --- | ---- |
| Random      | 9   | 1    |
| MM_Open     | 6   | 4    |
| MM_Center   | 7   | 3    |
| MM_Improved | 5   | 5    |
| AB_Open     | 3   | 7    |
| AB_Center   | 5   | 5    |
| AB_Improved | 5   | 5    |
__*Win Rate: 57.1%*__

## Conclusion
Based on the result, I would recommend to custom_score because it has
 not only highest win rate but also has stability if any opponent comes.