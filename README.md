# paper-notes
Some notes of papers I have read

Model-Free Episodic Control

Current RL algorithms:
DQN and A3C are designed for more general of stochasticity.
Evaluating the expected return is waste of time besides the gradient descent slows down it further.

Episodic Control:
records highly rewarding experience and follow a policy that replays sequences of actions that previously yielded high returns.

we limit the size of the table by removing the least recently updated entry once amaximum size has been reached.

update:
Q(s,a)=max(Q(s,a), R)

estimate novel state:
Q(s,a)=KNN from nearest k states, a is the same
