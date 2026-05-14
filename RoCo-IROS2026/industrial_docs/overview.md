# Industrial Board Assembly at RoCo Challenge @ IROS 2026
## 🌐 Challenge Overview
The RoCo Challenge evaluates Physical AI agents through collaborative robotic assembly. The competition focuses on robots that can reason, manipulate, act, and generalize in the physical world, rather than simply follow isolated commands.

RoCo evaluates agents across four core dimensions:

• **Physics Understanding**: The agent must understand physical interactions such as gravity, collision, deformation, friction, contact, and stability, then use that understanding to choose appropriate manipulation actions.

• **Dexterous Manipulation**: The agent must intentionally and effectively manipulate small, precise, and diverse components.

• **Long-horizon Reasoning**: The agent must plan and execute multi-step procedures, recover from failures, and remain aware of its own capabilities throughout a complex assembly task.

• **Generalizability**: The agent must learn, adapt, and generalize to unseen tasks, demonstrating robust intelligence rather than memorized behavior.

The Industrial Board Assembly track emphasizes practical deployment, dexterous manipulation, contact-rich assembly, and coordinated long-horizon execution on a task board inspired by the NIST task board.

To support different participant interests and research preferences, this track contains **two sub-tracks** using the same industrial task board but different robotic embodiments:

* **Sharpa North:** A versatile mobile manipulator with two robotic arms and 22-DoF dexterous hands, designed for a wide range of manipulation tasks.
* **DexMate Vega U:** An advanced bimanual robot with 7-DoF arms and grippers (UMI-supported), optimized for precision and contact-rich assembly tasks.

These two embodiments allow teams to explore both gripper-based manipulation and more challenging, highly promising dexterous manipulation. We encourage teams to participate in both sub-tracks and contribute their talents across both embodiment settings. Teams that use both embodiments to complete the task board assembly tasks will receive an extra bonus in the final score.

Simulation assets and real-robot data will be released for proper team usage. We are excited to provide participants with access to these leading robotic embodiments in meaningful and challenging industrial assembly tasks, supporting future applications of embodied AI.

---

## 🤺 Tasks
The robot must complete a sequence of industrial assembly operations on a task board. The same task board is used in both the **Sharpa North** and **DexMate Vega U** sub-tracks. The task board is designed to test perception, precision, contact-rich manipulation, and long-horizon autonomy.

### Trial Input
At the start of each trial, the robot is presented with:

* An empty industrial task board.
* A standardized kit area.
* Color-coded M4/M3 screws.
* Communication connectors, including RJ45, USB-A, USB-C, and HDMI.
* Industrial pins.
* Flexible cables.
* Three types of cylindrical batteries: D, AA, and AAA.
* A standardized bolt dispenser for screws.
* Simulation assets and real-robot data for developing, testing, and validating policies.

All components are pre-arranged in designated positions within the kit layout to ensure a fair and repeatable starting condition for every team.

### Procedure
The assembly sequence is strictly defined to simulate an industrial production line. During the trial, the robot must autonomously identify, pick, and assemble parts into their assigned regions. No human intervention is permitted after the procedure begins.

#### Task 1. Precision Screw Fastening
The robot retrieves and drives multi-specification screws into their corresponding threaded holes. The screws are color-coded by size.

A screw is considered successfully fastened when it is vertically stable and has sufficient thread engagement so that it cannot be extracted by axial force.

#### Task 2. Heterogeneous Connector Mating
The robot inserts multiple electrical interfaces, including RJ45, industrial pins, USB-A, USB-C, and HDMI connectors.

Each connector must be fully seated in its corresponding port, with robust mechanical engagement and electrical continuity.

#### Task 3. Cable Termination and Routing
The robot inserts cable terminals and routes flexible wires through the board's routing constraints.

The final cable layout should be organized, follow the designated path, and avoid snagging or displacement.

#### Task 4. Battery Installation
The robot installs D-cell, AA, and AAA batteries into their corresponding polarity-matched compartments.

The robot must determine the correct battery-to-compartment mapping using geometric and label cues, then place each battery with the correct polarity orientation.

The trial ends when the robot completes the full sequence or the maximum time limit is reached.

---

## 🧭 Score
Performance is evaluated using a hierarchical weighted scoring mechanism. The primary metric is the **Total Completion Score** `S_total`; the **Task Completion Time** `T` is used as a secondary tie-breaker.

The final score is the arithmetic mean of the normalized scores across the four functional procedures:

```
S_total = (1 / 4) * sum(n_i / N_i), for i = 1, 2, 3, 4
```

where:

* `i` represents one of the four procedures: screw fastening, connector mating, cable routing, and battery installation.
* `n_i` is the number of successfully assembled components in the `i`-th procedure.
* `N_i` is the total number of target assembly tasks assigned to the `i`-th procedure.
* `n_i / N_i` is the normalized performance index for that procedure, constrained to the range `[0, 1]`.

Each procedure contributes **25%** of the total score, regardless of the number of components involved. This balances high-precision tasks, such as HDMI insertion, with high-volume tasks, such as screw fastening.

### Successful Assembly Criteria
Within each procedure, a team earns one point for each successfully completed assembly unit:

* **Fastening (Q1)**: Each screw must exhibit vertical stability and resist axial extraction.
* **Connectors (Q2)**: Each connector, such as RJ45, USB, or HDMI, must be fully seated with confirmed mechanical engagement.
* **Routing (Q3)**: Each cable terminal must be inserted, and each wire must follow the designated path without displacement.
* **Batteries (Q4)**: Each battery must be placed in its corresponding housing with the correct polarity orientation.

If multiple teams achieve the same `S_total`, the team that achieved the score in the shortest duration `T` will be ranked higher.

Teams that complete the industrial board assembly tasks using both **Sharpa North** and **DexMate Vega U** will receive an additional bonus in the final score to recognize performance across both robotic embodiments.

## 🏅 Award

- 🥇: $10000

- 🥈: $5000

- 🥉: $2500


We invite all onsite teams to the award ceremony and networking event.
