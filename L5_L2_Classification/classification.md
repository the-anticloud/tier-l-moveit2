# L5 Narrow / L2 General Classification — L_MOVEIT2
**Platform:** Anticloud | **Tier:** TIER_9_ROBOTICS_IOT | **PAX:** 27B
**IP:** USPTO pending 2026, Anticloud FZ LLE, 0-1.gg | **License:** Apache-2.0

## L5 Narrow
L_MOVEIT2 integrates MoveIt 2 for Anticloud robot arm manipulation: collision-aware motion planning, trajectory execution, gripper control, and PAX 27B-guided task planning. Narrow scope: Anticloud robot arm platforms (UR, Franka, custom).

## L2 General
L2 General: L_MOVEIT2 provides manipulation capability for any Anticloud TIER_9 robot arm platform. Industrial automation and hospital delivery robots both use the same MoveIt 2 planning pipeline.

## PAX 27B Integration
PAX 27B provides task-level instructions to MoveIt 2: 'Pick up the red cylinder at position (0.3, 0.2, 0.1) in base frame. Approach from above, use soft grip (force: 5N max).' MoveIt 2 handles the motion planning.

## AIOSS Audit Chain
Every manipulation task (task hash + motion plan hash + collision check result hash + execution result hash) is chained: H_n = SHA3-256(H_{n-1} || entry_hash_n || timestamp_n).
Offline-verifiable, tamper-evident, zero cloud dependency.

## Regulatory / Compliance
ISO 10218 (robot safety). IEC 61508 (safety-critical motion). ISO 13482.
