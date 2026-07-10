# Industrial Board Assembly at RoCo Challenge @ IROS 2026
## 🌐 Challenge Overview
The RoCo Challenge evaluates Physical AI agents through collaborative robotic assembly. The competition focuses on robots that can reason, manipulate, act, and generalize in the physical world, rather than simply follow isolated commands.

RoCo evaluates agents across four core dimensions:

• **Physics Understanding**: The agent must understand physical interactions such as gravity, collision, deformation, friction, contact, and stability, then use that understanding to choose appropriate manipulation actions.

• **Dexterous Manipulation**: The agent must intentionally and effectively manipulate small, precise, and diverse components.

• **Long-horizon Reasoning**: The agent must plan and execute multi-step procedures, recover from failures, and remain aware of its own capabilities throughout a complex assembly task.

• **Generalizability**: The agent must learn, adapt, and generalize to unseen tasks, demonstrating robust intelligence rather than memorized behavior.

The Industrial Board Assembly track emphasizes practical deployment, contact-rich assembly, and coordinated long-horizon execution on a task board inspired by the NIST task board.

To support different participant interests and research preferences, this track contains **two sub-tracks** using the same industrial task board but different robotic embodiments:

* **DexMate Vega U:** A gripper-based bimanual robot with 7-DoF arms, optimized for precision pick-and-place and contact-rich assembly.
* **Sharpa North:** A dexterous hand-based mobile manipulator with two robotic arms and 22-DoF hands, designed for more flexible manipulation strategies.

Simulation assets and real-robot data will be released for participant use. We strongly encourage teams to participate in both sub-tracks and compete for awards in both the gripper-based and dexterous hand-based settings. To further support broad participation, we are also considering a proportional scoring method across sub-tracks so that every team has a fair opportunity to compete on both the DexMate Vega U and Sharpa North embodiments.

## Resources

* Simulation code repository: <https://github.com/rocochallenge/RoCo_TaskBoardAssembly>
* Simulation dataset using DexMate Vega U: <https://huggingface.co/datasets/rocochallenge2025/rocochallenge2026_Industrial_Assembly>
* Real-robot dataset using Sharpa North: <https://huggingface.co/datasets/SharpaIT/RoCo_TaskBoardAssembly>
* More datasets and resources will be released in the near future. Stay tuned!

---

## 🤖 Baselines

To help teams get started, the devkit ships multiple reference policy paths. They implement the same `Policy` interface (`task/policy_api.py`) and run through the standard harness, so you can benchmark against them or fork one as a starting point.

### Scripted baseline

`task/policies/baseline_scripted.py` is a rule-based reference: for each part it builds an end-effector waypoint path from `param_config.py`, follows it with Lula IK, and gates snap parts on the snap event. It needs no training and is the default policy:

```bash
uv run python task/run_pick_place.py \
    --policy policies.baseline_scripted.BaselinePolicy
```

Use it to sanity-check your setup and as a lower bound to beat.

### Learned baseline (Diffusion Policy)

For learning-based approaches, the devkit includes a worked example that trains a Diffusion Policy on the released dataset and deploys it in the harness:

1. **Data** — the released [HuggingFace dataset](https://huggingface.co/datasets/rocochallenge2025/rocochallenge2026_Industrial_Assembly) (LeRobot format: proprioceptive state + head/wrist RGB + actions).
2. **Train** — fit a Diffusion Policy on that dataset with [LeRobot](https://github.com/huggingface/lerobot).
3. **Deploy** — `task/policies/diffusion_lerobot.py` drives the `Policy` interface from the trained model. Because a torch/lerobot stack can't share Isaac Sim's interpreter, the model runs in its own venv and the adapter talks to it over a pickle pipe (`task/dp_server.py`).

```bash
DP_CKPT=/path/to/checkpoint/pretrained_model \
DP_SERVER_PY=/path/to/model-venv/bin/python \
uv run python task/run_pick_place.py \
    --policy policies.diffusion_lerobot.DiffusionLeRobotPolicy
```

This is a **reference pipeline to adapt, not a strong policy** — it shows how to wire a trained model end-to-end so you can drop in your own architecture, observation design, or training recipe. See the repository README ("Deploying a Learned Policy") for details.

### Learned baseline (pi0.5)

The devkit also supports evaluating LeRobot pi0.5 checkpoints through the same sidecar deployment pattern. This path is intended for teams that want to start from a vision-language-action policy rather than a compact diffusion baseline:

1. **Data** — use the released [HuggingFace dataset](https://huggingface.co/datasets/rocochallenge2025/rocochallenge2026_Industrial_Assembly), which provides the 44-D proprioceptive state, three RGB camera streams, and 14-D action labels.
2. **Fine-tune** — fine-tune a pi0.5 checkpoint in a LeRobot environment. The task repository documents the expected dataset/action layout and checkpoint format.
3. **Evaluate** — `task/policies/pi05_lerobot.py` runs inside Isaac Sim and talks to `task/pi05_server.py` running in the LeRobot environment. The bundled `scripts/eval_pi05_roco.sh` launcher records a rollout video and writes the standard results JSON.

```bash
LEROBOT_ROOT=/path/to/lerobot \
PI05_CUDA_VISIBLE_DEVICES=0 \
PI05_EVAL_MAX_STEPS=500 \
./scripts/eval_pi05_roco.sh /path/to/checkpoint/pretrained_model
```

The current pi0.5 adapter expects the released dataset action layout (`left xyz + left xyz Euler + left gripper + right xyz + right xyz Euler + right gripper`). The public runner still holds the right arm fixed by default, so the adapter executes the left 7-D slice during rollout. See the task repository's [pi0.5 eval guide](https://github.com/rocochallenge/RoCo_TaskBoardAssembly/blob/main/docs/pi05_eval.md) and README for setup details.

---

## 🤺 Tasks
The robot must complete a sequence of 9 industrial assembly operations on a task board. The harness walks `part_order` top-to-bottom, and each row below corresponds to one episode of `Policy.act` / `Policy.is_done`.

### Trial Input
At the start of each trial, the robot is given:

* A fixed task board with the target attachment locations already defined.
* One current part instance from `part_order`, evaluated in the order listed below.
* The release mode for that part: either `open` or `snap`.
* The corresponding scene state, including the board root and any target slot used for placement or snap evaluation.
* The part-specific success rule used by the harness: either position-based `grade_pos` or a successful snap event.

The current task set consists of the following 9 parts:

| # | name | source USD | release | snap target slot (parent body) | scoring |
|---|------|------------|---------|---------------------------------|---------|
| 1 | `gear_20teeth` | `parts/gear_20teeth.usdc` | open | — | `grade_pos` (mesh translate, <= 10 mm) |
| 2 | `gear_60teeth` | `parts/gear_60teeth.usdc` | open | — | `grade_pos` (mesh translate, <= 10 mm) |
| 3 | `rod_16mm` | `parts/rod_16mm.usdc` | snap | `task_board_color/root_001/_188_028` (w/ bolt) | snap fired |
| 4 | `bolt_8mm` | `parts/bolt_8mm.usdc` | snap | `task_board_color/root_001/_188_028` (w/ rod) | snap fired |
| 5 | `usb_a` | `parts/usb_a.usdc` | snap | `task_board_color` (board root) | snap fired |
| 6 | `hdmi` | `parts/hdmi.usdc` | snap | `task_board_color` (board root) | snap fired |
| 7 | `pin` | `parts/pin.usdc` | snap | `task_board_color/_188_001` | snap fired |
| 8 | `battery_size1` | `parts/battery_size1.usdc` | open | — | `grade_pos` (AABB midpoint, <= 10 mm) |
| 9 | `battery_size5` | `parts/battery_size5.usdc` | open | — | `grade_pos` (AABB midpoint, <= 10 mm) |

### Procedure
The assembly sequence is strictly defined by `part_order`, and the harness walks it from top to bottom. Each row in the table above corresponds to one episode of `Policy.act` / `Policy.is_done`.

For each part, the policy is expected to:

* Identify the current part in `part_order`.
* Pick the part from its initial scene location.
* Transport and align it with the correct target region or snap slot.
* Complete the required release behavior according to the part's mode.
* Satisfy the success condition for that part before moving to the next one.

For `open` parts, success is evaluated by `grade_pos`: the part must be placed so that the relevant mesh translation or AABB midpoint is within 10 mm of the target. For `snap` parts, success is achieved only when the part is aligned with the designated target slot and the snap event fires successfully.

`rod_16mm` and `bolt_8mm` should be treated as ordinary snap parts. Although `PERMANENT_PARTS = {bolt_8mm, rod_16mm}` remains defined in `param_config.py`, it is vestigial and is no longer consumed by the runner.

The trial ends after all 9 parts have been attempted or when the maximum time limit is reached.

---

## 🧭 Score
Each trial is scored by the number of successfully assembled parts, from 0 to 9.

The final score is the arithmetic mean of the assembled part counts across 10 independent trials:

```text
S_final = (1 / 10) * sum(n_k), for k = 1, ..., 10
```

where `n_k` is the number of successfully assembled parts in trial `k`.

### Successful Assembly Criteria
Each part contributes 1 point only when its current task-specific success condition is met:

* **`gear_20teeth`**: `grade_pos` succeeds using the mesh translation target, within 10 mm.
* **`gear_60teeth`**: `grade_pos` succeeds using the mesh translation target, within 10 mm.
* **`rod_16mm`**: the snap event fires successfully at `task_board_color/root_001/_188_028` together with the bolt counterpart.
* **`bolt_8mm`**: the snap event fires successfully at `task_board_color/root_001/_188_028` together with the rod counterpart.
* **`usb_a`**: the snap event fires successfully at the board root `task_board_color`.
* **`hdmi`**: the snap event fires successfully at the board root `task_board_color`.
* **`pin`**: the snap event fires successfully at `task_board_color/_188_001`.
* **`battery_size1`**: `grade_pos` succeeds using the AABB midpoint target, within 10 mm.
* **`battery_size5`**: `grade_pos` succeeds using the AABB midpoint target, within 10 mm.

If a part does not satisfy its success condition, it receives 0 points for that trial.

## 🏅 Award
Compete in a total of **$20K+** (Tentative) prize pool.

We invite all onsite teams to the award ceremony and networking event.
