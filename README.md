# HOMS-dataset
Robot manipulation task data for offline reinforcement learning (Offline RL) especially for the hierarchical object manipulation system (HOMS)

HOMS is a system for performing multi-tasks procedurally.

source code link: https://github.com/SunInKim/Hierarchical-Obejct-Manipulation-System-HOMS


The dataset is composed of a dataset for high-level policy (task classifier) and a dataset for low-level policy (robot controller).

------------
![re_Task_list](https://user-images.githubusercontent.com/50347012/145526995-172f883f-a5a0-4b97-9fc3-3774861342d1.png)

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
Each rollout contains 100 episodes of unit task.
## High policy (Task classifier)
### Structure
```
rollout
--episode
  --observations
  --actions
  --rewards
  --next_observations
  --terminals
  --possible_actions
```
### Data shape
```
observations: # goal_image+current_image (6, 240, 240) 
actions: # num_task (11,) 
rewards: # get 1 when possible action is None (1,)
next_observations: # goal_image+current_image (6, 240, 240)
terminals: # get 1 when possible action is None (1,)
possible_actions: # N is num_possible_action  (N,)
```

## Low policy (Robot controller)
### Structure
```
rollout
--episode
  --observations 
    --images
    --robot_state
  --actions 
  --rewards 
  --next_observations 
  --terminals 
  --tasks 
```
### Data shape
```
observations: # current_image (3, 240, 240), robot_state(x,y,z,yaw,grippersttate) (6,)
actions: # robot_action (x,y,z,yaw,gripper,task_terminal) (6,)
rewards: # get 1 for completing the task and returning to the initial position.  (1,)
next_observations: # current_image (3, 240, 240), robot_state (6,), task_id (10,)
terminals: # get done for completing the task and returning to the initial position.  (1,)
tasks: # one-hot vector which indicates the type of task (10,)
```

## Examples of transitions of each module to reach the goal state
### Goal state
![re_goal_state](https://user-images.githubusercontent.com/50347012/145527041-fb571c40-ec8f-4b92-b513-cfede163376e.png)
### Transition for task classifier
![re_task_select](https://user-images.githubusercontent.com/50347012/145527026-4b380dc3-7ac4-47d8-8b2c-ee4855210b0e.png)
### Transition for robot controller
![re_robot_control](https://user-images.githubusercontent.com/50347012/145527070-e10f93ba-555a-4acd-bf25-d47abf3c6b91.png)
