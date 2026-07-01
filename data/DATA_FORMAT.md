# Data format

Everything is in **metric metres**, in a **camera-centred** coordinate frame
(`+X` right, `+Y` down, `+Z` forward), consistent across the whole clip.

## `tracking.json`

```jsonc
{
  "metadata": {
    "fps": 15,
    "n_frames": 179,
    "image_width": 640, "image_height": 480,
    "camera": { "focal_px": 479.7, "cx": 320.0, "cy": 240.0, "model": "pinhole" },
    "gravity_up": [x, y, z],          // world up direction in camera frame
    "gravity_pitch_deg": -12.7,
    "gravity_roll_deg": -1.1,
    "coordinate_frame": "camera-centred, metres; +X right, +Y down, +Z forward",
    "hand_joint_order": "MANO 21: 0=wrist, thumb 1-4, index 5-8, middle 9-12, ring 13-16, pinky 17-20"
  },

  "objects": [                        // one entry per tracked object
    { "id": 0, "label": "black tool box", "detection_confidence": 0.945 }
  ],

  "frames": [
    {
      "frame": 0,
      "hands": [                      // 0-2 hands per frame
        {
          "side": "right",           // or "left"
          "joints_3d_m": [[x,y,z], … 21],   // 3D hand keypoints, metres
          "joints_2d_px": [[u,v],  … 21]    // same joints in image pixels
        }
      ],
      "objects": [
        {
          "id": 0, "label": "black tool box",
          "pose": {                          // 6DoF object pose (null if unavailable that frame)
            "rotation_3x3": [[…],[…],[…]],
            "translation_m": [x, y, z]
          },
          "obb": {                           // oriented 3D bounding box (null if unavailable)
            "corners_m": [[x,y,z], … 8],
            "extent_m": [dx, dy, dz]
          }
        }
      ]
    }
  ]
}
```

Notes
- `pose` / `obb` may be `null` on frames where an object is occluded or has too
  few visible points to fit a reliable box.
- Projecting 3D → 2D: `u = focal_px * X/Z + cx`, `v = focal_px * Y/Z + cy`.

## `hand_meshes/frame_NNNNNN.obj`

Standard Wavefront **OBJ**, one file per frame, openable in any 3D tool
(Blender, MeshLab, …). Each file contains the 3D hand mesh(es) for that frame
(778 vertices per hand, labelled `hand_left` / `hand_right`), in the same metric
camera frame as `tracking.json`.

## Available on request
Per-frame **metric depth maps** and **per-object segmentation masks** can be
provided if needed — not included here to keep the package light.
