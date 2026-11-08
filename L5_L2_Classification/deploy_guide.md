# Deploy Guide — L_MOVEIT2
**Tier:** TIER_9_ROBOTICS_IOT | **Stack:** Python 3.11, moveit2_tutorials, ROS2 Humble, PAX 27B, AIOSS_FORMAT
**Air-gap capable after initial setup.**

## Prerequisites
Python 3.11+, ROS2 Humble, MoveIt 2, robot_description URDF. T4 GPU for PAX planning.

## Environment
ROS2 Humble. MoveIt 2. Robot arm (UR, Franka, or sim). T4 GPU for PAX task planning.

## AIOSS Integration
```bash
aioss init --module L_MOVEIT2 --output ./l_moveit2.aioss
aioss append --chain ./l_moveit2.aioss --payload ./output.bin --module L_MOVEIT2
aioss verify --chain ./l_moveit2.aioss
```

## Air-Gap Setup
```bash
pip download -r requirements.txt -d ./wheels/
pip install --no-index --find-links ./wheels/ -r requirements.txt
```

## PAX 27B Harness Wiring
```python
from anticloud_pax import PAXHarness
harness = PAXHarness(
    model_path="./pax-27b-q4.gguf",
    module="L_MOVEIT2",
    aioss_chain="./L_MOVEIT2.aioss",
    classification="L5_NARROW_L2_GENERAL"
)
result = harness.process(input_data)
```

## Verification
```bash
aioss verify --chain ./L_MOVEIT2.aioss --verbose
python -m L_MOVEIT2.tests.smoke
```
