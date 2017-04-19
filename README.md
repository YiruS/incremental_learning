# HMM based Incremental Learning

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
  ![Alt text](/images/ITM.png?raw=true "Overview" =20*20) 
  ![](/images/ITM.png =100x20)

  * Updating structure
    1. For new node i, initialize prior i and self-transition a_i,i and state transition a_i,j, a_j,i.
  
    2. For deleted node and edge, assign zero to state prior and transition.
  
    3. Update emission mean.
  
  * Updating parameters
  
    ![Alt text](/images/params.png?raw=true "Update Parameters" =20*20) 
    ![](/images/params.png =100x20)

  
  
