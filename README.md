# Pirate Intelligent Agent — Deep Q-Learning (CS-370)

## Project Overview
This project implements a **deep Q-learning agent** that learns to navigate an 8x8
maze and find the "treasure." Starting with no knowledge of the maze, the agent
learns an optimal path purely through trial, error, and reward feedback, using a
neural network to estimate the value of each possible move.

## The Work: Given Code vs. My Code
I was **given** the supporting framework for the environment:
- `TreasureMaze.py` — the maze environment (state, valid moves, rewards, game status).
- `GameExperience.py` — the experience-replay memory that stores and samples past
  state–action–reward transitions.
- A starter Jupyter notebook containing the maze setup, the neural network
  `build_model()` function, and helper/visualization functions such as `play_game()`
  and `completion_check()`.

I **created** the core of the learning algorithm: the `qtrain()` deep Q-learning
training loop. My code:
- Runs training episodes, starting the agent from a random free cell each epoch.
- Implements the **epsilon-greedy** strategy (explore ~10% of the time, exploit ~90%),
  dropping epsilon to 0.05 once the win rate passes 0.9 to favor exploitation as the
  model converges.
- Stores each `(state, action, reward, next_state, status)` transition in the
  experience-replay buffer and trains the network on sampled batches.
- Uses a target network updated every 50 epochs for stable Q-value targets.
- Terminates training only after the agent hits a 100% win rate and passes the
  completion check, confirming it can reach the treasure from **every** free cell,
  not just a lucky subset.

## Reflection: Connecting This Work to Computer Science

**What do computer scientists do, and why does it matter?**
Computer scientists solve problems by turning messy, real-world situations into
models a machine can reason about, then designing algorithms that produce useful,
reliable results. This project is a small version of that: a search-and-navigation
problem became a reward function, a state space, and a learning loop. It matters
because the same reinforcement learning ideas used to solve a toy maze scale up to
real problems like robotics, logistics routing, and resource optimization — cases
where a system has to make good sequential decisions under uncertainty.

**How do I approach a problem as a computer scientist?**
I start by clearly defining the problem and its rules before writing code — here,
that meant understanding the states, the legal actions, and how rewards shape
behavior. I break the problem into parts (environment, memory, model, training loop)
and build on proven components rather than reinventing them. I then work iteratively:
tune one variable at a time (like the exploration-vs-exploitation ratio), test
against a measurable goal (win rate and the completion check), and use that feedback
to converge on a working solution. The biggest lesson from this course was that the
reward function *is* the design — the agent does exactly what you reward, so getting
the incentives right matters more than the network itself.

**What are my ethical responsibilities to the end user and the organization?**
My responsibility to the end user is to build systems that are correct, transparent,
and safe to rely on. In this project that meant not declaring success until the agent
was verified to solve the maze from every starting cell, so the result is genuinely
general rather than overfit to a few cases. To the organization, I am responsible for
writing clear, maintainable, well-documented code and being honest about a model's
limits. As these techniques move into higher-stakes domains, that same discipline —
validating thoroughly, avoiding overstated claims, and protecting the people affected
by the system's decisions — is what keeps the technology trustworthy.

## How to Run
Open `Jeremy_White_ProjectTwo.ipynb` in Jupyter, run the cells in order to build the
model and train the agent, then run the final cells to visualize the learned path.
