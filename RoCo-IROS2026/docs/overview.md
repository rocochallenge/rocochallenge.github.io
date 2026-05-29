# RoCo Challenge @ IROS 2026
## 🌐 Challenge Overview
The Gearbox assembly Assistance Challenge evaluates robotic systems in collaborative gearbox assembly within human-centric manufacturing environments. It targets scenarios where robots must work seamlessly with human operators. The challenge focuses on:

• **Prediction and Proactive Assistance**: Anticipating human requirements during assembly. 

• **Instruction Following**: Responding to gesture-based instructions. 

• **Error Detection and Correction**: Detecting errors, correcting them, and continuing the assembly correctly. 

• **Autonomous Continuation**: Autonomously completing assembly with generalized part placement.

Two complementary tracks are designed: **Simulation** and **Onsite Track**. The challenge aligns with IROS 2026 by emphasizing human–robot collaboration, error handling, and proactive assistance in complex manufacturing processes.

---

## 🤺 Competition Tracks

### 🖥️ Simulation Track — Human-in-the-Loop by State Initialization

Robots are evaluated in a simulated gearbox assembly environment where the human role is abstracted as initial conditions. A single Simulation Task is defined, but it may include the following representative scenarios:

•	**Assembly from Scratch**: Starting from an empty state, where the robot completes the assembly pipeline as its contribution to a joint workflow.

•	**Resume from Partial State**: The assembly has been partially completed by a “virtual human operator.” The robot must recognize the current state and continue to completion in the correct order.

•	**Error Detection and Recovery**: Errors are injected to mimic human mistakes. The robot must detect, remove incorrect parts, restore the valid state, and continue assembly.

### ⚒️Onsite Track — Human–Robot Collaborative Assistance
Robots collaborate with human operators under clear HRI protocols (e.g., gestures) on standardized physical kits and platforms. A single Onsite Task is defined, which may involve the following representative scenarios:

• **From-Scratch Physical Assembly:** Beginning from an empty state, with the robot responsible for executing the canonical gearbox assembly sequence.

• **Human-Aware Error Intervention:** While observing human assembly, the robot identifies mistakes, flags them in real time, performs safe corrections (remove/replace), and resumes the correct workflow.

• **Continuation and Proactive Assistance:** If the human leaves mid-task, the robot autonomously completes the remaining steps with part-placement generalization. While the human is present, it proactively provides part/tool hand-overs aligned with the current step to reduce idle time and cognitive load.

---

## 🧭 Gearbox Assembly Evaluation Metrics

## Overview
The benchmark evaluates robotic assembly performance through three tasks:

1. **Task 1 – Assembly from Scratch**  
   Complete the entire assembly sequence from an empty state.  

2. **Task 2 – Resume from Partial State**  
   Continue a few predefined steps from a partially assembled state.  

3. **Task 3 – Error Detection and Recovery**  
   Detect and remove incorrect parts, then continue assembly.  

Each task is scored from **0.0 – 1.0**.  
The **final score** applies a **4 : 2 : 4** weighting scheme:

`Final Score = (4*S1 + 2*S2 + 4*S3) / 10`

---

## Task 1 — Assembly from Scratch

S1 = (# correctly assembled parts) / (# total parts)


- Full completion → `S1 = 1.0`  
- Partial completion → proportional score  
- Parts assembled out of order are excluded from the correct count

---

## Task 2 — Resume from Partial State

S2 = (# successfully completed target steps) / N


- Each predefined step contributes `1/N`  
- Only the announced target steps are evaluated

---

## Task 3 — Error Detection and Recovery

S3 = 0.5 * (E_removed / E_total) + 0.5 * (P_correct / P_total)


where  
`E_removed` = number of incorrect parts removed,  
`E_total` = total incorrect parts,  
`P_correct` = number of correctly assembled parts after recovery,  
`P_total` = total parts in final state.  

## Definition of Parts and Assembly Correctness (Task 1–3)
A correctly assembled part is defined as a part that is successfully picked and placed at its intended target position with the correct spatial configuration. If a part is successfully picked but placed at an incorrect position or with an incorrect configuration, it is considered partially correct and receives a half-score (0.5). Parts that are not picked, are dropped, or remain incorrectly placed receive a score of 0.

---

## 📅 Time Schedule
**Cadence:** Proposal review → Simulation Competition → Onsite finalist selection → Ongoing preparation

- **June 22:** Proposal Deadline
- **June 29:** Pre-Finalists Announced
- **Now – August:** Simulation Competition
- **August 31:** Leaderboard Closes & Onsite Finalists Announced
- **Now – September:** Ongoing Preparation

#### General Policies:

- **Submission format:** Docker image + config + README; fixed seeds; Maximum of 3 submissions per week per team.
- **Revision control:** Evaluator is versioned; teams must declare the version used
- **Safety & ethics:** Onsite follows posted HRI & E-stop policy; violations result in immediate disqualification of the run
- **Comms:** FAQ updated weekly or as needed

---


## 🏢 Venue and Equipment
- **Locations:** Advanced Remanufacturing and Technology Centre (ARTC), Singapore

- **Equipment:** Standardized gearbox kits; robotic platforms (to be provided by the organizers, e.g., Galaxea); cameras, projector/display for live visualization

- **Software & Infrastructure:** Standardized deployment (Docker/ROS); high-speed internet access

---

## 📜 Participation and Rules
- **Teams:** 1–5 participants
- **Submission:** Code/models for simulation and real-world execution
- **Fairness:** All teams evaluated under identical conditions with standardized kits to ensure comparability and reproducibility
- **Evaluation:** Based on defined metrics; online track results shown on a public leaderboard and final rankings announced on-site

## 🏅 Award

- 🥇: $1000

- 🥈: $600

- 🥉: $400


Technical Sharing and Award Ceremony for the Top 2 Winning Teams






