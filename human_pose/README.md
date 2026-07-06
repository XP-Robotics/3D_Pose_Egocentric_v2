<div align="center">

# Egocentric 3D Human Pose

**XP Robotics**

Two-stage egocentric **3D human pose** estimation from **stereo fisheye RGB**,
predicting a **19-joint** 3D skeleton from a head/body-worn camera.

**Result: MPJPE 37.2 mm · PA-MPJPE 31.3 mm**

</div>

---

## Demo

<div align="center">

Input fisheye (left) · ground-truth skeleton (center) · **predicted** skeleton (right).

<img src="doc/demo.gif" width="90%">

▶️ [Full-resolution video](doc/demo.mp4)

</div>

---

## Pipeline at a glance

```
stereo fisheye RGB ──[Stage 1: heatmap net]──> 2D heatmaps ──[Stage 2: lifter]──> 19-joint 3D pose
```

| Stage | Input | Output |
|---|---|---|
| **1 · Heatmaps** | left + right RGB (256×256) | per-camera 2D joint heatmaps (64×64) |
| **2 · 3D lifting** | stereo heatmaps | 19 joints × 3 (cm), spine-centered |

**Joint set (19):** Hips, Spine, Chest, Neck, Head, and left/right Shoulder–Arm–ForeArm–Hand
and UpLeg–Leg–Foot.

---

## Output data

- Per-frame **19-joint 3D pose** (cm), spine-centered, left-camera frame
  (X right, Y down, Z forward)
- Convert normalized prediction → cm: `pose_cm = pred * std + mean`

---

## Credit

Architecture & base method: Akada et al., *UnrealEgo: A New Dataset for Robust
Egocentric 3D Human Motion Capture*, ECCV 2022 —
https://github.com/hiroyasuakada/UnrealEgo

```bibtex
@inproceedings{hakada2022unrealego,
  title     = {UnrealEgo: A New Dataset for Robust Egocentric 3D Human Motion Capture},
  author    = {Akada, Hiroyasu and Wang, Jian and Shimada, Soshi and Takahashi, Masaki and Theobalt, Christian and Golyanik, Vladislav},
  booktitle = {European Conference on Computer Vision (ECCV)},
  year      = {2022}
}
```

<div align="center"><sub>© XP Robotics — egocentric 3D human pose.</sub></div>
