# Capability Sheet — 3D Pose Egocentric

**XP Robotics** · Hand–Object 3D Reconstruction from a single RGB video

---

## What it does
From an ordinary RGB video of a person manipulating objects — **no depth sensor,
no calibration, no markers** — the system reconstructs a temporally consistent
3D understanding of the scene:

- **Metric depth** for every frame
- **3D hand meshes** for both hands (articulated, per frame)
- **Objects by text prompt** — detected, segmented, and tracked
- **6DoF object pose** + 3D bounding boxes over time
- **Robot retargeting** — the recovered hand motion mapped to a robot arm

Everything is produced in a single, gravity-aligned, metric world frame.

## Inputs
| Input | Notes |
|---|---|
| RGB video (mono) | short clip, static or slowly-moving camera |
| Object names (text) | e.g. `"black tool box"`, `"pressure gauge"` — no per-object training |

## Outputs (delivered)
| Output | Format |
|---|---|
| Hand-mesh overlay, 3D reconstruction, tracking videos | MP4 |
| Per-frame 3D + 2D hand keypoints, 6DoF object poses, 3D boxes | `tracking.json` |
| Per-frame 3D hand meshes | Wavefront `.obj` |
| Metric depth maps · object masks | MP4 (+ data on request) |
| Object 3D-trajectory plots · quality metrics | PNG · JSON |
| Robot arm trajectory + simulation | MP4 · `.npz` |

## Example results (this delivery)
- 12 s clip, 179 frames @ 15 fps
- **Both hands tracked on 100% of frames**
- **4 objects** detected + tracked by text prompt with high confidence
  (tool box 0.95, gauge 0.84, adapter 0.83, tool 0.69), 6DoF pose per frame
- Hand motion retargeted to a bimanual robot

## Why it matters
- **Sensor-free** — works from any existing RGB footage; no capture rig
- **Open-vocabulary** — any object, specified in plain language
- **Robot-ready** — perception connects straight to action (arm retargeting)
- **Structured, documented data** — not just visualizations; drop-in for
  downstream learning / analysis

---
© XP Robotics — capability demonstration.
