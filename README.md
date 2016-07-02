# paper-notes
Some notes of papers I have read

#[Model-Free Episodic Control](http://arxiv.org/abs/1606.04460), C. Blundell et al., *arXiv*, 2016.

###Current RL algorithms:

DQN and A3C are designed for more general of stochasticity.
Evaluating the expected return is waste of time besides the gradient descent slows down it further.

###Episodic Control:

records highly rewarding experience and follow a policy that replays sequences of actions that previously yielded high returns.

Tabular RL methods suffer from two key deficiencies: firstly, for large problems they consume a largeamount of memory, and secondly, they lack a way to generalise across similar states. 

we limit the size of the table by removing the least recently updated entry once amaximum size has been reached.

use KNN to generalise values across common experience.

##update:
Q(s,a)=max(Q(s,a), R)

##estimate novel state:
Q(s,a)=KNN from nearest k states, a is the same

![image](./model-free-episodic-control1.png =700x400)

Two phi functions:

* random projection

* Variational autoencoder

###Experiment details (read paper)

non-parametricmemorisation of experience VS parametric function approximators

###Questions

VAE implementation details