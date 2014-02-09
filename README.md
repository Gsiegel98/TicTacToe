Implementation of the classic game of Tic-Tac-Toe using Reinforcement Learning
=========

System Requirements: Python 2.7 or higher version

| Filename        | Description                                                                                |
|-----------------|--------------------------------------------------------------------------------------------|
| tictactoeRL.py  | user vs computer game                                                                      |
| tictactoeRL2.py | computer vs computer (This is how the program learns)                                      |
| tictactoe.dat   | contains data for computer player 1 and is the same data used during user vs computer game |
| tictactoe2.dat  | contains data for computer player 2 during computer vs computer game                       |


Section 1.4 in the textbook (Reinforcement Learning, Sutton & Barto), provides an explanation on how to approach the [Tic-tac-toe](http://en.wikipedia.org/wiki/Tic-tac-toe) problem using reinforcement learning. I followed the initial estimated state values as explained in the book, where a no-win, win, and draw/lose states will have the corresponding intial state values of 0.5, 1, and 0 respectively. The algorithm is setup to move greedily but has a 10% chance of doing an exploratory move. 

During the game, the state-values are updated in our attempt to get the actual estimates of the winning probability. In order to do this, we "back up" the previous state-value only during greedy moves. This rule is based on temporal-difference learning method using the notation:


V(s) <- V(s) + a[V(s') - V(s)]     

Where: 
* s    = state before the greedy move
* s'   = state after the move 
* V(s) = estimated value of s
* a    = learning rate (0.1)


Observations:

Initially, I had my game play against a player whose moves are randomly selected. Doing 200,000 to 300,000 episodes, the computer player intial moves are not converging fast enough and there are still some simple moves that computer player still loses. When I start playing against the computer, after continuously doing the same sequence of moves and winning, the computer player eventually learns to block but not fast enough. This is when I realize that my random player is not challenging my computer player enough for it to converge faster to its winning probabilities.

In Exercise 1.1 (Self-play), reading the exercise gave me the idea of having my algorithm play against itself. So I made a copy of the states for each player and had them play against each other for 100,000 episodes. The results were remarkable, after the learning phase, the computer converges to its winning probabilites with a very low rate of wrong moves, and such wrong moves where mostly attributed to exploratory moves. I decided to add 100,000 more episodes and the results on how many times player 1 and 2 wins as well as the number of draws came out to be equally proportionate.


References:
"Reinforcement Learning, An Introduction" by Richard S. Sutton and Andrew G. Barto. 
