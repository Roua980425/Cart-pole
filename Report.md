# Introduction
In this project we aim to train the agent to balance a CartPole which is a game in which you try to balance the pole as long as possible. It is assumed that at the tip
of the pole, there is an object which makes it unstable and very likely to fall over. The goal of this project is to move the cart left and right so that the pole
can stand (within a certain angle) as long as possible.<br />
The state is represented by 4 values : 
* cart position
* cart velocity
* pole angle
* velocity of the tip of the pole

The agent can take one of two actions at every step

* moving left 
* moving right

The longer you keep the pole standing, the more score you will get.
The game is over when the pole exceeds 12-degree angle or the cart is going out of the screen.
# Learning Algorithms
### DQN (Deep Q Network):<br />
There is a problem with Q-Learning, that is the state space is huge. Each small change to the angle of the pole or the velocity of the cart represents a new state. We would need to have a very big memory to store all possible states. This is why Q-Learning by itself is not enough to get the job done. To cope with this problem, we need something to approximate a function that takes in a state-action pair (s,a) and returns the expected reward for that pair. That is when deep learning comes in. It is renowned for approximating a function just from the training data. So we implemented the DQN algorithm.<br />
We used replay buffer for training our DQN. It stores the transitions that the agent observes, allowing us to reuse this data later. By sampling from it randomly, the transitions that build up a batch are decorrelated. It has been shown that this greatly stabilizes and improves the DQN training procedure.<br />

![Pseudo-code-of-DQN-with-experience-replay-method-12](https://user-images.githubusercontent.com/68075541/148925603-5ab93cb1-e9f1-4d93-a160-42bca9576355.png)


### Double DQN:<br />
The agent uses two neural networks to learn and predict what action to take at every step. 
* One network(local network), referred to as the Q network or the online network, is used to predict what to do when the agent encounters a new state(to select actions). 
* And then we used the target network for retrieving the q values since its values are kept steadyas fixed q targets and to break correlations between the predicted and the target value and to update the weights of the target.<br />
Also we have a replay buffer because we receive at each time step a tuple composed by the state, the action, the reward, and the new state so in order to make our agent learn from the past policies, every tuple is stored in the replay buffer.<br />

![1_4B46Bc9EDUdwrnqhAUp7hQ](https://user-images.githubusercontent.com/68075541/148843211-3b531be6-9880-49bf-921b-c344fec22111.png)



# Model Architecture
* The network of the DQN agent have the following architecture:

  1. 1 hidden layer : dense layer of size 100
  2. 1 output layer : dense layer of size 2 (the size of the action space)
 
* The Double DQN agent has a target and local networks having the same architecture:

   1. 1 hidden layer : dense layer of size 100
   2. 1 output layer : dense layer of size 2 (the size of the action space)

# Hyperparameters
Our agent was trained using the follwing hyperparameters:<br />
* Buffer size: the size of the experience replay buffer is 10 000 <br />
* Gamma: the discount factor 0.97<br />
* Batch size: 50<br />
* TAU Learning rate coefficient(DDQN): 0.01<br />
* The agent is updated after every 2 time steps<br />

# How to train our Model
* For the DQN agent: We train the dqn agent for 400 episodes, for each episode we start by giving the initial state of our environment to the agent, the total rewards and if it is in the last state or not. If not, so during training we will call our "train" function after each step in the environment that gives us next state, reward and done(boolean variables mean we are in the last state or not)<br />
* For the DDQN agent: For each episode, we start by giving the initial state of our environment to the agent, initialize the "total_rewards" to zero and the "done" variable to false. Then, for each time step we give our agent the current state of our environment and it will return the action that he will perform(the next state), the total rewards and if we are in the last state or not. We have 10 run, 200 episodes per run and 2 steps per episode.<br />

# Results
This is the result of the dqn agent:<br />
![train1](https://user-images.githubusercontent.com/68075541/148851482-e87f7fb0-bd71-4b65-a0ea-5c598e54696e.PNG)<br />

The figure below present a comparisation between DQN training result and DDQN training result
![dqn vs ddqn](https://user-images.githubusercontent.com/68075541/148851425-cc3f548c-2adb-46f0-a86f-ecb20a23d976.PNG)

