# Deep Reinforcement Learning Project 
## Introduction : 
#### Description :
A pole is attached by an un-actuated joint to a cart, which moves along
a frictionless track. The pendulum starts upright, and the goal is to
prevent it from falling over by increasing and reducing the cart's
velocity. 

![Alt text](https://tenor.com/view/reinforcement-learning-cartpole-v0-tensorflow-open-ai-gif-18474251.gif)

#### Source :
This environment corresponds to the version of the cart-pole problem
described by Barto, Sutton, and Anderson

#### Observation : 
        Type: Box(4)
        Num     Observation               Min                     Max
        0       Cart Position             -2.4                    2.4
        1       Cart Velocity             -Inf                    Inf
        2       Pole Angle                -0.209 rad (-12 deg)    0.209 rad (12 deg)
        3       Pole Angular Velocity     -Inf                    Inf
 
 #### Actions :
 * Push cart to the left
 * Push cart to the right
 
 #### Reward :
 Reward is 1 for every step taken, including the termination step
 (+1 is provided for every timestep that the pole remains upright)
 
 #### Starting state :
 * Pole Angle is more than 12 degrees.
 * Cart Position is more than 2.4 (center of the cart reaches the edge of the display).
 * Episode length is greater than 200.
 * Solved Requirements:
        Considered solved when the average return is greater than or equal to
        195.0 over 100 consecutive trials.
## Getting start :
To run the code in your jupyter notebook you should :

1. Install Gym 
 
        !pip install gym
 
2. Install Pyglet

        !pip install pyglet

## Train the agent :
In order to train the agent you have to:

1. Initialize the agent
2. Evaluate state and action space
3. Train the agent using Deep Q-Networks (DQN)
4. Iterate for 400 epochs

You can train the agent following the instructions in the notebook DeepQNetworksInOpenAIGym.ipynb.

You can also train the agent using Double Deep Q-Networks following the instructions in the notebook DoubleDQNsInOpenAIGym.ipynb.

