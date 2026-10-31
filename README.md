# Minidrone Vision-Based Line Following (MATLAB/Simulink)

Flight control and computer vision for the **Parrot Minidrone Competition**
(MathWorks). The drone uses its downward camera to follow a line track
autonomously in Simulink.

![MATLAB](https://img.shields.io/badge/MATLAB-0076A8?logo=mathworks&logoColor=white)
![Simulink](https://img.shields.io/badge/Simulink-0076A8)
![Control](https://img.shields.io/badge/Control-MPC%20%2B%20PD-555)

## Architecture

```
Downward camera (120×160)
   │  binarize + erode
   ▼
Vision detector       → finds a look-ahead point on the track
   ▼
Path planner (outer)  → MPC-style setpoints, holonomic "crab" motion, fixed heading
   ▼
Attitude / yaw PD (inner loop) → motor thrust and torques
```

## What I built

- Line detector with crown mask, branch commitment and behind-point exclusion,
  so the drone does not jump between branches at junctions
- Outer-loop planner (`controller/mpc_racing_controller.m`) that moves the drone
  sideways toward the track without yawing, which removed the spin/tumble
  problems seen when yaw control was active
- Tuning notes and full documentation in
  [`CONTROL_VISION_MANUAL.md`](CONTROL_VISION_MANUAL.md) (Thai)

## Run

Requires MATLAB with the **Simulink Support Package for Parrot Minidrones**.
Open `MinidroneCompetition.prj`, run `startVars`, then run the model.

## Author

Sirapop Poonkaew, Control Systems & Instrumentation Engineering, KMUTT
