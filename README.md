# Learning Local Transition Rules of 2D Multi-State Cellular Automata via Least Squares Estimation
Cellular automata like Conway's Game of Life represent simplified models of complex systems with local interactions. This project proposes to bridge cellular automata with recent advances in learning interaction laws of agent-based systems. By treating the 3D Game of Life with multiple cell types as an agent-based system with discrete states, we can apply and adapt methodologies to infer both network structure and interaction rules from observation data.
Cellular automata (CA) provide simplified yet powerful models for studying complex systems governed by local interactions. Extending classical models like Conway's Game of Life, this project investigates the inference of local, deterministic transition rules for a multi-state three-dimensional cellular automata (CA) using simulated trajectory data. We specificallly address on the inverse problem of learning the rules governing state changes based on a cell's current state and local neighborhood features (neighbor counts). We adapt methodologies from probabilistic cellular automata, formulating the rule inference as a supervised learning task. A Least Squares Estimator (LSE) framework is employed to learn the mapping from local features to the next discrete cell state. The framework developed provides a data-driven approach for analyzing and understanding the local dynamics governing complex discrete systems.

Author: Siyang Sun, Xinming Shen, Yue Yu

The Final_script.ipynb has our final attempt and all functions classes. The folder has some save/load attempts intended for future scalability. 


### References
1. https://arxiv.org/abs/cond-mat/0106649
2. https://pubmed.ncbi.nlm.nih.gov/33730201/
3. https://arxiv.org/html/2405.02928v2
2. https://www.sciencedirect.com/science/article/pii/S0303264799000891 （thanks to Melody J）


