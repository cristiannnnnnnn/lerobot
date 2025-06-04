# Teleoperate
python lerobot/scripts/control_robot.py \
  --robot.type=so101 \
  --robot.cameras='{}' \
  --control.type=teleoperate

# with cams
python lerobot/scripts/control_robot.py \
  --robot.type=so101 \
  --control.type=teleoperate \
  --control.display_data=true


  HF_USER=$(huggingface-cli whoami | head -n 1)
echo $HF_USER


# record dataset

python lerobot/scripts/control_robot.py \
  --robot.type=so101 \
  --control.type=record \
  --control.fps=30 \
  --control.single_task="Move from A to B to resting position" \
  --control.repo_id=${HF_USER}/so101_test001 \
  --control.tags='["so101","test"]' \
  --control.warmup_time_s=5 \
  --control.episode_time_s=30 \
  --control.reset_time_s=10 \
  --control.num_episodes=50 \
  --control.display_data=true \
  --control.push_to_hub=true

# train

# eval

python lerobot/scripts/control_robot.py \
  --robot.type=so101 \
  --control.type=record \
  --control.fps=30 \
  --control.single_task="Move from A to B to resting position" \
  --control.repo_id=${HF_USER}/eval_act_so101_test001 \
  --control.tags='["so101","test"]' \
  --control.warmup_time_s=5 \
  --control.episode_time_s=30 \
  --control.reset_time_s=10 \
  --control.num_episodes=10 \
  --control.push_to_hub=true \
  --control.policy.path=outputs/train/act_so101_test001/checkpoints/last/pretrained_model