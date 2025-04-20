# Learning Network Structure and Interaction Rules in a 3D Cellular Automaton with Multiple Cell Types

## Project Proposal

### 1. Introduction

Cellular automata like Conway's Game of Life represent simplified models of complex systems with local interactions. This project proposes to bridge cellular automata with recent advances in learning interaction laws of agent-based systems. By treating the 3D Game of Life with multiple cell types as an agent-based system with discrete states, we can apply and adapt methodologies to infer both network structure and interaction rules from observation data.

### 2. Background

#### 2.1 Theoretical Foundation

Recent research has made significant progress in learning interaction laws in agent-based systems. These works establish powerful mathematical frameworks for solving inverse problems in agent-based systems, where the goal is to discover the underlying rules from observations of system dynamics.

#### 2.2 Cellular Automata as Agent Systems

Cellular automata can be viewed as special cases of agent-based systems where:
- Agents (cells) have fixed positions
- States are discrete rather than continuous
- Interactions occur on a regular grid structure
- Rules are typically deterministic (though can be made stochastic)

The 3D Game of Life with multiple cell types presents an ideal testbed for adapting and applying the methodologies from recent research.

### 3. Project Objectives

1. Design a 3D extension of Conway's Game of Life with two distinct cell types
2. Formulate a ground truth interaction kernel with known rules
3. Generate synthetic trajectory data from simulations
4. Adapt and apply ALS and ORALS algorithms to infer network structure and interaction rules
5. Evaluate inference accuracy and analyze factors affecting learning performance
6. Demonstrate connections between cellular automata and agent-based learning methods

### 4. Methodology

#### 4.1 System Design

We propose a 3D cellular automaton with three possible states for each cell:
- Dead (state 0)
- Type A (state 1)
- Type B (state 2)

The neighborhood structure includes 26 adjacent cells in a 3×3×3 cube (excluding the center). The ground truth system will use a subset of these neighbors, which the learning algorithms will attempt to identify.

#### 4.2 Interaction Kernel Design

To align with research on distance-dependent interactions, we define summary statistics that capture the configuration of neighbors:

- N₁, N₂, N₃: Number of Type A neighbors at face, edge, and corner distances
- M₁, M₂, M₃: Number of Type B neighbors at face, edge, and corner distances

The ground truth kernel maps these features and the current state to the next state:

For Type A cells:
- Survive if: 2 ≤ (N₁ + 0.7·N₂ + 0.4·N₃) ≤ 3.5 AND (M₁ + 0.7·M₂ + 0.4·M₃) < 2
- Transition to Type B if: (M₁ + 0.7·M₂ + 0.4·M₃) ≥ 2
- Otherwise die

For Type B cells:
- Survive if: 1.5 ≤ (M₁ + 0.7·M₂ + 0.4·M₃) ≤ 4 AND (N₁ + 0.7·N₂ + 0.4·N₃) < 3
- Otherwise die

For Dead cells:
- Become Type A if: 2.8 ≤ (N₁ + 0.7·N₂ + 0.4·N₃) ≤ 3.2 AND (M₁ + 0.7·M₂ + 0.4·M₃) < 1
- Become Type B if: 2.8 ≤ (M₁ + 0.7·M₂ + 0.4·M₃) ≤ 3.2 AND (N₁ + 0.7·N₂ + 0.4·M₃) < (M₁ + 0.7·M₂ + 0.4·M₃)
- Otherwise remain dead

This design incorporates several key features from advanced research:
- Distance-dependent weighting
- Heterogeneous interactions between different cell types
- Thresholds that create nonlinear behavior

#### 4.3 Data Generation Approach

We will generate synthetic data through:
1. Multiple simulation runs with varied initial conditions
2. Recording cell states and transitions at regular intervals
3. Computing feature vectors for each cell based on neighborhood configurations
4. Creating labeled datasets of (features, current_state) → next_state pairs

#### 4.4 Learning Algorithms

We will adapt two key algorithms:

**1. Adapted ALS (Alternating Least Squares):**
- Initialize with full connectivity (all 26 neighbors)
- Alternately optimize:
  - Fix network structure, learn interaction rules using classification methods
  - Fix interaction rules, optimize network structure with regularization for sparsity
- Iterate until convergence

**2. Adapted ORALS (Operator Regression with ALS):**
- Build an operator that maps the entire state space forward in time
- For discrete systems, formulate as a classification problem
- Use regularization to discover sparse network structure
- Apply alternating optimization to refine both components

The key adaptation for both algorithms is replacing continuous regression with classification methods suitable for discrete systems.

#### 4.5 Evaluation Methods

We will evaluate learning performance through:

1. **Prediction accuracy:**
   - How accurately the learned model predicts state transitions
   - Confusion matrices for transition classification

2. **Network recovery:**
   - Precision/recall in identifying which neighbors truly matter
   - Comparison of learned weights with ground truth weights

3. **Dynamic behavior:**
   - Long-term pattern formation in simulations with learned rules
   - Statistical properties of emergent structures
   - Stability analysis of the learned system

### 5. Expected Challenges and Solutions

#### 5.1 Discrete vs. Continuous Systems

**Challenge:** The methods are designed for continuous-state systems with smooth kernels.

**Solution:** Adapting the methods using classification instead of regression, and exploring probabilistic transitions to create smoother function spaces.

#### 5.2 Curse of Dimensionality

**Challenge:** The full configuration space of 26 neighbors with 3 possible states is enormous.

**Solution:** Using summary statistics (our 6 features) to significantly reduce dimensionality while preserving critical information.

#### 5.3 Identifiability

**Challenge:** Multiple rule sets might produce similar observed behavior.

**Solution:** Applying regularization to prefer simpler models and using multiple trajectories to better constrain the solution space.

### 6. Significance and Impact

This project contributes to both cellular automata research and agent-based learning methods by:

1. Demonstrating that methods from agent-based learning can be adapted to discrete systems
2. Providing a test case for joint network and kernel inference in a controlled setting
3. Establishing connections between two research communities
4. Potentially revealing insights about rule inference in discrete complex systems

The methodologies developed could be applied to real-world discrete systems such as:
- Gene regulatory networks
- Social contagion processes
- Neural network activation patterns
- Ecological community dynamics

### 7. Conclusion

This project proposes to bridge cellular automata with recent advances in learning interaction laws of agent-based systems. By treating the 3D Game of Life with multiple cell types as an agent-based system, we can apply and adapt methodologies to infer both network structure and interaction rules from observation data. This work not only demonstrates the broad applicability of these learning methods but also establishes new connections between discrete and continuous complex systems research.
