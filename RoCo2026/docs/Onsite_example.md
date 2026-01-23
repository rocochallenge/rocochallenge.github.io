# EFMNode

EFMNode is the reference robot control node we use for the Roco Challenge 2026. It
integrates vision-language models (VLM) with robot action inference for real-time robot control via ROS2.
It provides a modular framework combining:

- ROS2 communication (subscribers/publishers)
- Multi-camera + proprioception observation fusion
- Model inference (Diffusion Policy / VLA / RL policies / LLM-assisted control)
- Action scheduling & trajectory execution
- A plugin-based processing pipeline

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
    # Ensure ROS2 is sourced
    source /opt/ros/humble/setup.bash

# How the Node Works (Architecture Overview)

EFMNNode is structured around the following modules (from your uploaded code), please refer to these codes for your usage or own code construction:

### core/communication/robot_topics.py
    Centralized configuration for all state / image / action topics
    Defines QoS prof
    Configures deque buffer lengths
    Maps topic types → R1 Lite ROS message types

### core/communication/ros2_bridge.py
    Subscribing to all sensors (RGB images, joint states, EE poses)
    Publishing all robot actions
    Timestamp alignment & nearest-message search
    Gathering multimodal observations → dict



### core/inference/inference_engine.py (only for galaxea G0 model inference)
    Defines a clean interface:
    load_model()
    predict_action(batch)
    Device management (cuda/cpu)
    Warmup and batch preprocessing hooks




### scheduler/scheduler.py (only for galaxea G0 model inference)
    Main responsibilities:
    Gather observations from Ros2Bridge
    Apply processor preprocessing
    Run inference model
    Map model predictions to robot topics
    Generate trajectories
    Publish actions at control_frequency

### Pseudo-flow:
    # while ros2 ok:
    obs = ros2_bridge.gather_obs()
    instruction = instruction_manager()
    batch = processor.preprocess(obs)
    actions = inference_engine.predict_action(batch)
    execute trajectory to robot via ros2_bridge.publish_action()

### reset.py: Provides low-level “return arms to rest position” functionality using pure ROS2 publishers. 
    python /home/pine/galaxeavla_finetune_assembly/EFMNode/scripts/reset.py
    
    
# On-site Notifications

## File and environment management

All teams should only store their codes and checkpoints under the **~/roco/[teamname]** , and any changes outside this directory should ask for organizer's assistance.

If conda is used, all teams should only create and edit their own conda environments named **roco_[teamname]_[serial]**. Any edit to base and other teams' environment is not allowed. Any installation to system or ros2 python should ask for organizer's assistance.

Any edit to system variables and paths are not allowed, and adding new varialbes should ask for organizer's assistance.
