# 🎯Baseline Training & Fine-tuning
We provide several options of baseline training, for comparison to your own policies.

## Training Options

### ACT
For the environment installation, please refer to the GitHub repository of ACT.
```bash
git clone https://github.com/tonyzhaozh/act.git
```
To train ACT
```bash
python3 imitate_episodes.py \
--task_name <task name in the constanst.py> \
--ckpt_dir <ckpt dir> \
--policy_class ACT --kl_weight 10 --chunk_size 100 --hidden_dim 512 --batch_size 8 --dim_feedforward 3200 \
--num_epochs 2000  --lr 1e-5 \
--seed 0
```

#### Usage Example
We have supported ACT rollout as an example in our environment, just run this command
```bash
# use 'FULL_PATH_TO_isaaclab.sh|bat -p' instead of 'python' if Isaac Lab is not installed in Python venv or conda
python scripts/VLA_agent.py --task=Template-Galaxea-Lab-Agent-Direct-v0 --enable_cameras --checkpoint='Your-VLA-Checkpoint-File-Path'
```
Use this realization as a reference for deploying your own policies.

Modify the task in `constants.py`
