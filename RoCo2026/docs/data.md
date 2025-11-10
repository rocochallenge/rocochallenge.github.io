# 🦾 RoCoChallenge2026 Dataset

## 📘 Overview

The **RoCoChallenge2026** dataset is part of the **AAAI 2026 Human-Centric Manufacturing Workshop Challenge**, focusing on **collaborative gearbox assembly**.  
It contains synchronized multimodal observations and actions collected from a **bimanual robotic platform** performing human-robot collaborative assembly tasks.  

---

## 📂 Dataset Access

We host our dataset on **Hugging Face**.

**Dataset URL:**  
👉 [https://huggingface.co/datasets/rocochallenge2025/rocochallenge2025](https://huggingface.co/datasets/rocochallenge2025/rocochallenge2025)


## 📊 Data Description

| Group | Dataset | Shape | Description |
|-------|----------|--------|--------------|
| `/actions` | `left_arm_action` | (N, 7) | Left arm Cartesian + gripper actions |
| `/actions` | `right_arm_action` | (N, 7) | Right arm Cartesian + gripper actions |
| `/observations` | `left_arm_ee_pose` | (N, 7) | Left arm end-effector pose (xyz + quaternion) |
| `/observations` | `right_arm_ee_pose` | (N, 7) | Right arm end-effector pose (xyz + quaternion) |
| `/observations` | `left_arm_joint_position` | (N, 6) | Left arm joint positions (radians) |
| `/observations` | `right_arm_joint_position` | (N, 6) | Right arm joint positions (radians) |
| `/observations` | `left_arm_joint_velocity` | (N, 6) | Left arm joint velocities |
| `/observations` | `right_arm_joint_velocity` | (N, 6) | Right arm joint velocities |
| `/observations` | `left_gripper_position` | (N, 1) | Left gripper open ratio |
| `/observations` | `right_gripper_position` | (N, 1) | Right gripper open ratio |
| `/observations` | `rgb_head` | (N, 240, 320, 3) | Head-mounted RGB camera frames |
| `/observations` | `rgb_left_hand` | (N, 240, 320, 3) | Left wrist RGB camera frames |
| `/observations` | `rgb_right_hand` | (N, 240, 320, 3) | Right wrist RGB camera frames |


Each sample corresponds to one synchronized time step in a demonstration sequence.
