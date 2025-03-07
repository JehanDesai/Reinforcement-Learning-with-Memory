# Reinforcement-Learning-with-Memory


Reinforcement Learning for Audit Decision-Making Using GRU and Attention
This project implements a Reinforcement Learning (RL) model to optimize audit decision-making by training an agent to determine whether to audit or skip based on six risk factors. The RL agent is built using Deep Q-Networks (DQN) with GRU (Gated Recurrent Units) and Attention Mechanism, ensuring efficient learning from sequential data while focusing on the most relevant information.

Environment Setup: Simulating Audit Risk
The environment is implemented using OpenAI Gym and simulates an auditing scenario where each case has six numerical risk factors.

The state space consists of a 6-dimensional vector representing risk factors.
The action space includes two choices: Audit (1) or Skip (0).
A weighted sum of the risk factors determines the risk score, and rewards are assigned based on whether the decision aligns with the risk level.
The episode terminates after a predefined number of steps.

Deep Q-Network Agent with GRU and Attention


To train an intelligent audit agent, we implement a Deep Q-Network (DQN) with GRU and Attention.

WHY?? -> DQN alone is powerful, but it lacks the ability to handle sequential dependencies and efficiently focus on key information. DQN is great for learning optimal Q-values through experience replay, but it treats each state as independent.

        No Memory → DQN does not retain information from previous states.
        Flat Representation → It assumes that the current state contains all necessary information.
        Inefficient for Temporal Dependencies → Tax audits are often based on patterns over time, which DQN cannot naturally capture.

GRU (Gated Recurrent Unit) solves the memory issue by allowing the model to retain past information.


        Maintains Historical Context → GRU remembers patterns in risk factors over multiple steps.
        Detects Fraudulent Behavior Over Time → Instead of treating each case as new, it tracks evolving risk trends.
        Handles Partial Observability → Some risk factors might not be clear in a single step, but GRU helps infer missing details from past audits.


Even though GRU helps retain past states, it treats all past information equally, which is inefficient.

Some past events are more important than others for making decisions.
Attention helps the model focus on critical risk factors instead of treating all past cases equally.

        Selectively Focuses on Key Events → Instead of using all past states, it assigns more weight to significant ones.
        Improves Decision Accuracy → Helps the model audit cases with actual high risk instead of being overwhelmed by irrelevant past data.
        Enhances Explainability → We can interpret which risk factors influenced the audit decision.


GRU (Gated Recurrent Unit) handles sequential data, allowing the agent to retain past information.
Attention Mechanism enhances decision-making by assigning higher importance to critical risk factors.
The model architecture includes:

    -> A GRU layer to process sequential risk data.

    -> An Attention layer to determine which past states are most relevant.
  
    -> Fully connected layers (FC layers) for Q-value prediction.
  
    -> During training, the agent learns optimal decision-making strategies by exploring various audit cases and adjusting its policy.

Reinforcement Learning Process: Training the Audit Agent
The agent is trained using the Deep Q-Learning algorithm, following these steps:

      -> Experience Replay: The agent stores past experiences in memory and samples random batches for training, reducing correlation between consecutive decisions.
  
      -> Epsilon-Greedy Exploration: The agent initially explores different actions randomly but gradually shifts towards exploiting learned strategies by reducing exploration over time.
      
      -> Q-Learning Updates: The model updates Q-values using the Bellman equation, ensuring future rewards influence present decisions.
      
      -> Gradient Descent Optimization: The network minimizes prediction errors using Mean Squared Error (MSE) loss and Adam optimizer.

Evaluation & Visualization of Agent Performance
After training, the agent is evaluated on new audit cases to assess decision-making efficiency.

      -> Performance Metrics: The agent's total rewards over multiple episodes are tracked to measure improvement.
      
      -> Action Distribution Plot: Displays how often the agent chooses to audit or skip cases.
      
      -> Risk Level vs. Action Scatter Plot: Shows the correlation between risk factors and the agent’s decisions, ensuring logical alignment with the model’s learning.
      
      -> Exploration Decay: The gradual reduction in random actions ensures that the agent transitions from exploration to exploitation.

Saving & Testing the Model
The trained RL model is saved and reloaded for future use.
A random case assessment function runs new cases through the model, demonstrating real-time decision-making.
