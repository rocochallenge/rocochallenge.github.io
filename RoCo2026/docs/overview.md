# RoCo Challenge @ AAAI 2026
## 🌐 Challenge Overview
The Gearbox assembly Assistance Challenge evaluates robotic systems in collaborative gearbox assembly within human-centric manufacturing environments. It targets scenarios where robots must work seamlessly with human operators. The challenge focuses on:

• **Prediction and Proactive Assistance**: Anticipating human requirements during assembly. 

• **Instruction Following**: Responding to gesture-based instructions. 

• **Error Detection and Correction**: Detecting errors, correcting them, and continuing the assembly correctly. 

• **Autonomous Continuation**: Autonomously completing assembly with generalized part placement.

Two complementary tracks are designed: **Simulation** and **Onsite Track**. The challenge aligns with HCM-AAAI26 by emphasizing human–robot collaboration, error handling, and proactive assistance in complex manufacturing processes.

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

## 📋 Evaluation Metrics
**Metrics applied to both tracks:**

• **Task Success Rate:** Each trial is scored on a normalized scale between 0 and 1.

– A score of 1.0 is assigned if the assembly is fully completed and the assembly order is correct.

– For partially completed assemblies, the score is computed as the ratio of correctly assembled components to the total number of components (score = #assembled / #total).

This metric jointly captures the effectiveness of robotic assembly strategies, accounting for both full and partial task completion while ensuring correct assembly sequencing.


## 📅 Time Schedule
**Cadence:** Preparation → Public Release → Online Competition (Simulation track) → Onsite Finals (Onsite track)


### Phase A · Public Release — Nov 10, 2025
- **Open:** Team registration; simulation submission portal.
- **Publish:** Website, rules v1.0, dataset, evaluator, baselines; leaderboard policy.
- **Comms:** Kick-off webinar & FAQ v1.0.

### Phase B · Online Competition (Simulation) — Nov 10, 2025 → Jan 10, 2026
- **Submission cadence:** Rolling; leaderboard refresh bi-weekly (Fri 18:00 UTC)
- **Checkpoints:**
  - Rules Freeze: Dec 10, 2025 — thereafter only clarifications.
  - CP-1: Dec 13, 2025 — interim reportable results (auto-archived).
  - CP-2 (final online): Jan 10, 2026 — last leaderboard submission.
- **Required package (Teams):** Docker image + logs; short method card (≤2 pages)
- **Evaluation:** Reproducibility re-runs for top-k; anomaly review
- **Shortlist Notification:** Jan 12, 2026 — finalists invited to onsite

### Phase C · Onsite Finals (Real-World) — Jan 24-26, 2026
#### Day 1 — Team Setup & Calibration ( Jan 24 )

- **Welcome & Briefing** (~20 min)  
  Opening remarks, competition overview, and safety protocol introduction.

- **System Registration & Workspace Assignment** (~20 min)  
  Team check-in, workspace allocation, and hardware verification.

- **Team Calibration Sessions (Teams 1–3)** (3 × 2 h)  
  Each team receives a 2-hour slot for setup, robot calibration, and HRI protocol rehearsal.

- **Lunch / Networking Break** (~1.5 h)  
  Informal interaction among teams, judges, and organizers.

- **Team Calibration Sessions (Teams 4–6)** (3 × 2 h)  
  Environment integration, perception tuning, and dry-run validation for remaining teams.

- **System Integration Check** (~1 h)  
  Unified review

---

#### Day 2 — Onsite Finals & Demonstrations ( Jan 25 )

- **Final Briefing & Readiness Review** (~30 min)  
  Confirmation of competition environment and evaluation procedure.

- **Unified Model Testing Phase** (~3–4 h)  
  All teams execute standardized test cases using the final models submitted at the end of Day 1; reproducibility and fairness verified by judges.

- **Official Onsite Trials** (~3 h)  
  Sequential evaluation of all teams following the unified testing stage; task success, assembly-order correctness recorded.

- **Metric Computation & Feedback Session** (~1 h)  
  Judges compute normalized task scores, review logs, and prepare preliminary ranking.
---


#### Day 3 — AAAI Workshop & Award Session ( Jan 26 )

- **Award Ceremony @ AAAI Venue** (~30 min)  
  Top 3 teams recognized at the AAAI HCM Workshop plenary; certificates and prizes presented.

- **Technical Talks by Top 2 Teams** (~1 h)  
  Invited presentations on system design, policy architecture, and lessons learned during the RoCo Challenge.

- **Panel Discussion & Closing** (~30 min)  
  Round-table with organizers and participants on future directions of human-robot collaboration benchmarks.

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


