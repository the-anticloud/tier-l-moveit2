# Developer Cookbook — L_MOVEIT2
**Stack:** Python 3.11, moveit2_tutorials, ROS2 Humble, PAX 27B, AIOSS_FORMAT
**Domain:** MoveIt 2: robot arm motion planning for Anticloud manipulation tasks

## PAX-guided manipulation
```python
from l_moveit2 import AnticloudMoveIt

planner = AnticloudMoveIt(
    robot_description="./ur5_description/",
    pax_model="./pax-27b-q4.gguf",
    aioss_chain="./moveit2.aioss"
)

# PAX generates pick-and-place task
task = planner.pax_plan_task(
    instruction="Pick up the blue bottle from the table and place it in bin A",
    scene_description=current_scene  # from L_ISAACROS
)
print(f"Task steps: {len(task.steps)}")

# Execute
result = planner.execute(task, safety_check=True)
print(f"Success: {result.success}, Collisions: {result.n_collisions}")
print(f"Chain: {result.chain_hash}")
```

## AIOSS Chain Append
```python
import hashlib, time

def aioss_append(chain_path, payload: bytes, module_id: str):
    entry_hash = hashlib.sha3_256(payload).digest()
    ts = int(time.time_ns()).to_bytes(8, 'big')
    with open(chain_path, 'rb') as f:
        f.seek(-32, 2); prev_hash = f.read(32)
    new_hash = hashlib.sha3_256(prev_hash + entry_hash + ts).digest()
    with open(chain_path, 'ab') as f:
        f.write(ts + entry_hash + new_hash)
    return new_hash.hex()
```
