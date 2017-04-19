# HMM based Incremental Learning
======

## [Growing Hidden Markov Models: AN Incremental Tool for Learning and Predicting Human and Vehicle Motion.](http://journals.sagepub.com/doi/pdf/10.1177/0278364909342118)

  Notes: This paper learns incrementally both the **stucture** and **parameters** of HMM.
  
  Assumptions: 
  
  1. observation sequences correspond to complete examples (i.e. from beginning to end) of the whole process or system being modeled          (e.g. in our application this corresponds to complete pedestrian trajectories).
  
  2. The evolution of the state of the modeled system or process is a continuous function.
  
  3. **The observation space is a subspace of the continuous state space. This implies that, by finding a decomposition of the          observation space, a decomposition is also performed on the continuous state space.** 
  
  Assump3 is the most important, which allows to use observation sequence for adapting HMM structure(#states, state transition, emission).
  
  ### Three Updates
 
  ![Alt text](/images/overview.png?raw=true "Overview")
  * Updating topological map (instantaneous topological map ITM) 
  ![Alt text](/images/ITM.png?raw=true "Overview") 

  * Updating structure
    1. For new node i, initialize prior i and self-transition a_i,i and state transition a_i,j, a_j,i.
  
    2. For deleted node and edge, assign zero to state prior and transition.
  
    3. Update emission mean.
  
  * Updating parameters
  
    ![Alt text](/images/params.png?raw=true "Update Parameters") 
  
  ## [Incremental Learning,Clustering and Hierarchy Formation of Whole Body Motion Patterns using Adaptive Hidden Markov Chains.](http://journals.sagepub.com/doi/pdf/10.1177/0278364908091153)

  Notes: Autonomous and incremental learning of motion pattern from human motions using Factorial HMMs.
  1. The model size (#chains in FHMM) is adaptable based on density of the motion data in the regions.
  
  2. As new motion patterns (data) are observed, they are incrementally grouped together using **hierarchical agglomerative clustering** based on their relative distance in the model space. The clustering algorithm forms a # tree structure #, with specialized motions at the tree leaves, and generalized motions closer to the root. The generated tree structure will depend on the type of training data provided, so that the most specialized motions will be those for which the most training has been received.
  
  ![Alt text](/images/FHMM_overview.png?raw=true "FHMM overview") 
  
  (a) a newobservation sequence is observed and encoded as an HMM
  
  (b) the observation sequence is compared to existing groups via tree search
  
  (c) the new sequence is placed in the closest existing group
  
  (d) local clustering is performed on the modified group 
  
  (e) a new subgroup is formed from similar motions in the modified group
  
  (f) the subgroup is added to the tree as a child of the modified group.
  
  Following is the pseudocode for clustering.
  ![Alt text](/images/FHMM_pseudocode.png?raw=true "FHMM clustering") 
  
  **When comparing model distance (case b and case c in last figure), there are four conditions:**
  
    1. If the distance between the new observation (encoded by an HMM) and the cluster (encoded by FHMM or HMM, depending on data complexity) is larger than Dthresh, this cluster will not be considered as a possible match for the new observation sequence. 
    
    2. If there are multiple candidate clusters, the new sequence is placed in the closest cluster. 
    
    3. If there are no candidates, the new sequence is placed in the parent cluster. 
    
    4. In the case of a new motion pattern which is completely dissimilar to any existing motion patterns, the motion pattern will be placed into the root node.
    
  **When a new observation sequence is added to a cluster, a clustering procedure is invoked on that group, to determine if a subgroup may be formed.**
  If so, a new group model is trained using the raw observation sequences from all the group elements. The structure of the new group model is determined based on the maximum intra observation distance for group, D_max. **Additional chains** are added based on a simple threshold evaluation.
  
  **Evaluations.**
  
  1. Compare log likelihood of HMM and FHMM for data of the same motion type in training set, the same motion outside the training set, and of a different motion. (Useful comparison, can be used in my paper.)
  2. Compare FHMM with two independent HMM chains, proving FHMM is not simply the combined two independent HMM chains. Instead, chains in FHMM are dependent on the observation, which makes it powerful obtaining data/observation characteristics. 
  
  Following is an example of tree structure of 9 motions.
  
  ![Alt text](/images/FHMM_tree_example.png?raw=true "FHMM tree") 
  
  ## [Online Segmentation and Clustering From Continuous Observation of Whole Body Motions.](http://ieeexplore.ieee.org/stamp/stamp.jsp?arnumber=5175268)
  
  Notes: Observed time series data is **automatically** segmented into motion segments by **building HMM over a window of previous observations** and finding the optimum state sequence over the model. => Optimum state sequence is the desired segmentation. 
  Clustering is used the same method in *Incremental Learning,Clustering and Hierarchy Formation of Whole Body Motion Patterns using Adaptive Hidden Markov Chains.*
  
