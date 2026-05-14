# Brick Assembly at RoCo Challenge @ IROS 2026
## 🌐 Challenge Overview
The RoCo Challenge uses brick assembly to assess Physical AI agents across four core dimensions:

• **Physics Understanding**: The agent must grasp fundamental real-world physics, including gravity, collisions, deformation, friction, and structural stability. Grounded in this understanding, the agent must perform appropriate physical actions, such as aligning components properly, applying sufficient assembly force, and avoiding excessive force that could break the structure.

• **Dexterous Manipulation**: The agent must intentionally and effectively manipulate objects. Given the tiny sizes of the bricks and the high precision required, dexterous manipulation is a critical capability for successful task completion.

• **Long-horizon Reasoning**: The agent must execute complex tasks requiring extended planning. True intelligence extends beyond simple command-following; the agent must understand the overarching objective, reason through the necessary steps, and execute a sequence of appropriate actions.

• **Generalizability**: The agent must be able to learn, adapt, and generalize to unseen tasks, demonstrating genuine intelligence rather than rote memorization.
The combinatorial nature of brick assembly unlocks an **infinite task space**, making it an ideal platform for evaluating generalizability.



---

## 🤺 Tasks

The Brick Assembly track features **two distinct evaluation tasks**. While all tasks require a solid grasp of physics and dexterous manipulation, the required reasoning capability progressively increases with each task. Initial setups are provided for all tasks to ensure an equal and standardized evaluation.

### Task 1. Step Reasoning
This task tests the agent's ability to perform a single-step assembly (e.g., successfully placing a single brick at a target location).

#### **Input**: 

* `structure_start.json`: The initial assembly structure.
* Image renderings of the initial assembly structure from 30 different viewpoints.
* `structure_goal.json`: The goal assembly structure.
* Image renderings of the goal assembly structure from 30 different viewpoints.

#### **Evaluation Metric**: 

Pass/Fail. The agent receives **1 point** for successfully achieving the goal structure, and 0 points otherwise.

#### **Example**: 

Coming soon!


### Task 2. Sequence Reasoning
This task requires the agent to assemble a goal structure from scratch. The final structural layout is provided, but no step-by-step guidance is given. The agent must reason and plan the assembly sequence accordingly.

#### **Input**: 

* `structure.json`: The goal assembly structure.
* Image renderings of the goal assembly structure from 30 different viewpoints.


#### **Evaluation Metric**: 

We compare the assembled structure against the goal structure. The score is calculated as the number of correctly assembled bricks.

#### **Example**: 

Coming soon!


---

## 🧭 Score

The **final score** for the Brick Assembly track will be calculated as 

`Final Score = (S1 + S2_1^2 + S2_2^2 + S_3^2 + ... + S_N^2)`

where S1 is the total score achieved by completing type-1 tasks and S2_i is the score by completing the i-th task in type-2 tasks.


---

## 🧱 Brick Representation
We represent a brick assembly structure using a JSON dictionary. Each node represents a distinct brick in the structure with the following format:
```
"id": {
    brick_id,
    x,
    y,
    z,
    ori,
    color
    }
``` 
where `brick_id` denotes the brick type, `x, y, z` are the brick relative position in the structure. `ori` is the brick orientation and `color` is the [color code](https://rebrickable.com/colors/) indicating the color of the brick. In this challenge, we will have 7 types of bricks, including *1x2, 1x4, 1x6, 1x8, 2x2, 2x4, and 2x6*, with different colors.

---

## 🏅 Award

- 🥇: $10000

- 🥈: $5000

- 🥉: $2500

- In-kind awards for all onsite teams.


We invite all onsite teams to the award ceremony and networking event.






