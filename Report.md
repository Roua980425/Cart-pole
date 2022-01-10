# Introduction
In this project we aim to train the agent to balance a CartPole which is a game in which you try to balance the pole as long as possible. It is assumed that at the tip of the pole, there is an object which makes it unstable and very likely to fall over. The goal of this project is to move the cart left and right so that the pole can stand (within a certain angle) as long as possible.
the state is represented by 4 values — cart position, cart velocity, pole angle, and the velocity of the tip of the pole — and the agent can take one of two actions at every step — moving left or moving right.
The longer you keep the pole standing, the more score you will get. The game is over when the pole exceeds 12-degree angle or the cart is going out of the screen.
# Learning Algorithms
DQN (Deep Q Network):
There is a problem with Q-Learning, that is the state space is huge. Each small change to the angle of the pole or the velocity of the cart represents a new state. We would need to have a very big memory to store all possible states. This is why Q-Learning by itself is not enough to get the job done. To cope with this problem, we need something to approximate a function that takes in a state-action pair (s,a) and returns the expected reward for that pair. That is when deep learning comes in. It is renowned for approximating a function just from the training data. So we implemented the DQN algorithm.
We used replay buffer for training our DQN. It stores the transitions that the agent observes, allowing us to reuse this data later. By sampling from it randomly, the transitions that build up a batch are decorrelated. It has been shown that this greatly stabilizes and improves the DQN training procedure.
![Pseudo-code-of-DQN-with-experience-replay-method-12](https://user-images.githubusercontent.com/68075541/148843222-5acfd8a8-5b90-4263-81ef-135fe545ee04.png)

Double DQN:
The agent uses uses two neural networks to learn and predict what action to take at every step. One network(local network), referred to as the Q network or the online network, is used to predict what to do when the agent encounters a new state(to select actions). And then we used the target network for retrieving the q values since its values are kept steadyas fixed q targets and to break correlations between the predicted and the target value and to update the weights of the target.
Also we have a replay buffer because we receive at each time step a tuple composed by the state, the action, the reward, and the new state so in order to make our agent learn from the past policies, every tuple is stored in the replay buffer
![1_4B46Bc9EDUdwrnqhAUp7hQ](https://user-images.githubusercontent.com/68075541/148843211-3b531be6-9880-49bf-921b-c344fec22111.png)



# Model Architecture

# Hyperparameters
Our agent was trained using the follwing hyperparameters://
Buffer size: the size of the experience replay buffer is 10 000//
Gamma: the discount factor 0.97
Batch size: 50
TAU Learning rate coefficient(DDQN): 0.01
The agent is updated after every 2 time steps

# How to train our Model
for the DQN agent: We train the dqn agent for 400 episodes, for each episode we start by giving the initial state of our environment to the agent, the total rewards and if he is in the las state or not.if not so during training we will call our agent train function after each step in the environment that gives us next state, reward and done(bolean variables mean we are in the last step or not)
for the DDQN agent: For each episode, we start by giving the initial state of our environment to the agent, the total rewards and if he is in the las state or not. Then, for each time step we give our agent the current state of our environment and he will return the action that he will perform(the next state), the total rewards and if we are in the last state or not.(we have 10 run, 200 episodes per run and 2 steps per episode).

# Results
this is the result of the dqn agent:
![train1](https://user-images.githubusercontent.com/68075541/148851482-e87f7fb0-bd71-4b65-a0ea-5c598e54696e.PNG)
![dqn vs ddqn](https://user-images.githubusercontent.com/68075541/148851425-cc3f548c-2adb-46f0-a86f-ecb20a23d976.PNG)

