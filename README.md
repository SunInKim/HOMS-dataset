# HOMS-dataset
Robot manipulation task data for offline reinforcement learning especially for the hierarchical object manipulation system (HOMS)
source code link : --

The dataset is composed of a dataset for high policy (task classifier) and a dataset for low policy (robot controller).

HOMS is a system for performing multi-tasks procedurally.

------------
1. Laptop close     
2. Drawer open 
3. Drawer close 
4. Box open
5. Box close
6. Box push
7. Green to space
8. Green to drawer
9. Orange to space
10. Orange to box
11. Tasks complete
------------

data link: https://drive.google.com/drive/folders/17LdN5XEarPH81re-2-bMEcZzkTaRVmHD?usp=sharing

# Collection method
The dataset is collected using pybullet simulator.

The scripted policy can be found in env.util.task_policy.py

The dataset can be collected by execute the code

```p
python get_rollout.py
```

# Description of the dataset
## High policy (Task classifier)
### Structure
```
rollout
--observations
--actions
--rewards
--next_observations
--terminals
--possible_actions
```
### Data shape
```
observations: (6, 240, 240) # goal_image, current_image
actions: (11,) # num_task
rewards: (1,) # get 1 when possible action is None
next_observations: (6, 240, 240) # goal_image, current_image
terminals: (1,) # get 1 when possible action is None
possible_actions: (N,) # N is num_possible_action
```

## Low policy (Robot controller)
### Structure
```
rollout
--observations
--actions
--rewards
--next_observations
--terminals
--tasks
```
### Data shape
```
observations: (3, 240, 240) # current_image
actions: (6,) # (x,y,z,yaw,grip,task_end)
rewards: (1,) # get 1 when task is done and task_end>0.5
next_observations: (3, 240, 240) # current_image
terminals: (1,) # get 1 when task is done and task_end>0.5
tasks: (11,) # one-hot vector indication what kind of task it is
```
