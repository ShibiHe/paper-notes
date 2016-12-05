# paper-notes
Some notes of papers I have read

* [Model-Free Episodic Control](#paper1)
* [Deep Successor Reinforcement Learning](#paper2)
* [Massively Parallel Methods for Deep Reinforcement Learning](#paper3)
* [Asynchronous Methods for Deep Reinforcement Learning](#paper4)

<a name="paper1">
#[Model-Free Episodic Control](http://arxiv.org/abs/1606.04460), C. Blundell et al., *arXiv*, 2016.
##This paper is so interesting that I am trying to implement the algorithm on Github [Github: Model-Free-Episodic-Control](https://github.com/ShibiHe/Model-Free-Episodic-Control).
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

![image2](https://github.com/ShibiHe/paper-notes/blob/master/Model-Free-Episodic-Control2.png =600x100)

##estimate novel state:
Q(s,a)=KNN from nearest k states, a is the same


![image3](https://github.com/ShibiHe/paper-notes/blob/master/Model-Free-Episodic-Control3.png =600x100)

##algorithm

![image](https://github.com/ShibiHe/paper-notes/blob/master/model-free-episodic-control1.png =600x350)

Two phi functions:

* random projection

* Variational autoencoder

###Experiment details (read paper)

non-parametricmemorisation of experience VS parametric function approximators

###Questions

VAE implementation details

###My thoughts
episodic control uses KNN while DQN uses neural network. DQN's training procedure is time consuming but it is quick when it is in running procedure. Episodic control needs KNN to evaluate Q(s,a) when running.
</a>

<a name="paper2">
# [Deep Successor Reinforcement Learning](http://arxiv.org/abs/1606.02396), T. D. Kulkarni et al., *arXiv*, 2016.

related paper: [Improving Generalisation for TemporalDifference Learning:The Successor Representation](http://www.gatsby.ucl.ac.uk/~dayan/papers/d93b.pdf)

The value function of a state can be computed as the inner product between the successor map and the reward predictor weights.
</a>

<a name="paper3">
  
# [Massively Parallel Methods for Deep Reinforcement Learning](http://www0.cs.ucl.ac.uk/staff/d.silver/web/Publications_files/gorila.pdf), A. Nair et al., ICML Workshop, 2015.

###review of DQN
![image1](https://github.com/ShibiHe/paper-notes/blob/master/Massively Parallel Methods for Deep Reinforcement Learning1.png =500x400)

![image1](https://github.com/ShibiHe/paper-notes/blob/master/Massively Parallel Methods for Deep Reinforcement Learning2.png =400x100)

![image1](https://github.com/ShibiHe/paper-notes/blob/master/Massively Parallel Methods for Deep Reinforcement Learning3.png =400x100)

Two differences between Q-Learning and DQN

* experience delay
* separate Q network and Target Q network (Q' is fixed and updated periodically)

### Gorila DQN
Actor 

Experience delay (local or global)

Learners

Parameter Server which uses DistBelief [(Large Scale Distributed Deep Networks)](https://papers.nips.cc/paper/4687-large-scale-distributed-deep-networks.pdf)

The Gorila architecture provides considerable flexibility in the number of ways an RL agent may be parallelized. It is possible to have parallel acting to generate large quantities of data into a global replay database, and then process that data with a single serial learner.  In contrast, it is possible to have a single actor generating data into a local replay memory, and then have multiple learners process this data in parallel to learn as effectively as possible from this experience.  However, to avoid any individual component from becoming a bottleneck, the Gorila architecture in general allows for arbitrary numbers of actors, learners, and parameter servers to both generate data, learn from that data, and update the model in a scalable and fully distributed fashion.

</a>
 
<a name="paper4">

# [Asynchronous Methods for Deep Reinforcement Learning](http://arxiv.org/pdf/1602.01783v2.pdf), V. Mnih et al., arXiv, 2016.

By  running  different  exploration policies in different threads, the overall changes be-ing made to the parameters by multiple actor-learners applying online updates in parallel are likely to be less correlated in time than a single agent applying online updates.Hence, we do not use a replay memory and rely on parallel actors employing different exploration policies to perform the stabilizing role undertaken by experience replay in theDQN training algorithm.

###Asynchronous one-step Q-learning
![image1](https://github.com/ShibiHe/paper-notes/blob/master/Asynchronous Methods for Deep Reinforcement Learning1.png =500x600)

1. accumulate gradients over multiple time steps just like mini batch
2. fixed target Q network the same as DQN
3. giving each thread a different exploration policy helps improve robustness (epsilon samples from some distribution for every thread)

###Asynchronous one-step SARSA

change r+discount * max(Q(s',a')) to r+discount * max(Q(s',a'))


</a>
  