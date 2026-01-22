# EFMNode

EFMNode is a robot control node that integrates vision-language models (VLM) with robot action inference for real-time robot control via ROS2.
It provides a modular framework combining:

- ROS2 communication (subscribers/publishers)
- Multi-camera + proprioception observation fusion
- Model inference (Diffusion Policy / VLA / RL policies / LLM-assisted control)
- Action scheduling & trajectory execution
- A plugin-based processing pipeline

---

## Table of Contents
- [Environment Setup](#environment-setup)
- [Model Weights and Configuration](#model-weights-and-configuration)
- [Running and 
####Data Recording](#running-and-data-recording)
- [Troubleshooting](#troubleshooting)

---

## Environment Setup

### Prerequisites

- ROS2 Humble


### Installation Steps

---

1. **Clone the EFMNode repository**:
```bash
cd EFMNode
```

2. **Clone and install the GalaxeaFM repository** (if not already done):
```bash
git clone https://github.com/OpenGalaxea/GalaxeaVLA.git
cd GalaxeaFM
uv sync --index-strategy unsafe-best-match
uv pip install -e .
source .venv/bin/activate
cd ..
```


### Running 
### Ensure ROS2 is sourced
    source /opt/ros/humble/setup.bash



# How the Node Works (Architecture Overview)

EFMNNode is structured around the following modules (from your uploaded code):

### core/communication/robot_topics.py
    Centralized configuration for all state / image / action topics
    Defines QoS profiles
    Configures deque buffer lengths
    Maps topic types → R1 Lite ROS message types



### (core/communication/ros2_bridge.py)
### Responsible for:
    Subscribing to all sensors (RGB images, joint states, EE poses)
    Publishing all robot actions
    Timestamp alignment & nearest-message search
    Gathering multimodal observations → dict



### (core/inference/inference_engine.py)
### only for galaxea G0 model inference
### Defines a clean interface:
    load_model()
    predict_action(batch)
    Device management (cuda/cpu)
    Warmup and batch preprocessing hooks




### (scheduler/scheduler.py)
### only for galaxea G0 model inference
### This is the brain of your system.
### Main responsibilities:
    Gather observations from Ros2Bridge
    Apply processor preprocessing
    Run inference model
    Map model predictions to robot topics
    Generate trajectories
    Publish actions at control_frequency
### Pseudo-flow:
### while ros2 ok:
    obs = ros2_bridge.gather_obs()
    instruction = instruction_manager()
    batch = processor.preprocess(obs)
    actions = inference_engine.predict_action(batch)
    execute trajectory to robot via ros2_bridge.publish_action()

### reset.py: Provides low-level “return arms to rest position” functionality using pure ROS2 publishers. 
    python /home/pine/galaxeavla_finetune_assembly/EFMNode/scripts/reset.py
    
    



