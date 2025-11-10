# 🎯Baseline Training & Fine-tuning
We provide several options of baseline training, for comparison to your own policies.

## Training Options

### ACT
For the environment installation, please refer to the GitHub repository of ACT.
```bash
git clone https://github.com/tonyzhaozh/act.git
```
Convert hdf5 to satisfy the act's training format
```bash
python ./data_preprocess_act.py
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
Modify the task in `constants.py`