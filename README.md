# Animal-Inspired Hand-Tracked VR Locomotion

A Unity prototype that lets users control bird-like flight through hand tracking. Hand poses and palm orientation select flight behaviors, while inverse kinematics maps tracked hand motion to a rigged bird avatar.

**Game Interactive Technology · Kyung Hee University · Spring 2024 · Team project**

[Project demo](https://youtu.be/f_mEII5rgyE)

## Interaction concept

The project explores how an animal-motion metaphor can connect hand gestures with movement in a virtual environment. In the bird-flight prototype, users bring their hands together to activate flight, then flap or tilt their hands to move.

The implementation combines:

- **Hand tracking:** wrist positions and palm orientation provide control signals.
- **A finite-state controller:** gestures select gliding, flapping, turning, descent, and deceleration.
- **Avatar feedback:** Two-Bone IK and animation connect hand input to the bird's pose.
- **A navigation task:** checkpoints, direction cues, and a timer support the demo.

The repository also contains a teleportation scene. The original concept considered other animal locomotion modes; this repository's documented prototype focuses on bird flight.

## Controls

| Action | Input |
| --- | --- |
| Activate flight | Hold the configured glide hand pose with both hands and bring the wrists close together. |
| Glide | Maintain the active pose without triggering another flight state. |
| Ascend | Make a flapping motion. |
| Turn | Roll the palms. |
| Descend or decelerate | Change palm pitch; the direction determines the selected state. |
| Deactivate flight | Separate the wrists. |

Gesture definitions and thresholds are configured in the scene and the assets under `Assets/TEST/Hand poseshape/`.

## Environment

The course prototype was developed with a **Meta Quest 3**. The committed project specifies **Unity 2022.3.22f1**.

| Package | Version in `Packages/manifest.json` |
| --- | --- |
| XR Interaction Toolkit | 2.5.2 |
| XR Hands | 1.4.1 |
| Animation Rigging | 1.2.1 |
| OpenXR | 1.10.0 |
| Meta OpenXR | 1.0.1 |
| Oculus XR Plugin | 4.2.0 |
| Input System | 1.7.0 |
| Universal Render Pipeline | 14.0.10 |

## Open and run

1. Download or clone this repository.
2. Install **Unity 2022.3.22f1** through Unity Hub, including **Android Build Support**, **Android SDK & NDK Tools**, and **OpenJDK**.
3. Open the repository root in Unity Hub—the folder containing `Assets/`, `Packages/`, and `ProjectSettings/`—and let Unity restore the packages.
4. Open the bird-flight scene:

   ```text
   Assets/final_demo/Scene/final_demo_bird.unity
   ```

5. In **File → Build Settings**, select **Android** and switch platforms if necessary. Add the open scene to the build and remove or disable `SampleScene`.
6. Connect a Quest configured for development, enable hand tracking, and use **Build and Run**.

**Scene selection matters:** the committed build list contains only `Assets/Scenes/SampleScene.unity`, so building without changing it will not launch the bird demo.

The committed Android configuration uses OpenXR, ARM64, IL2CPP, and minimum API level 29. These instructions follow the archived project settings; a fresh headset build has not been verified for this re-hosted snapshot.

To inspect the teleportation scene, open:

```text
Assets/final_demo/Scene/final_demo_teleporation.unity
```

The filename above preserves the spelling used in the repository.

## Code map

| Path | Role |
| --- | --- |
| `Assets/TEST/ValueMonitoring.cs` | Computes hand separation, palm orientation, and flapping-related input values. |
| `Assets/TEST/BirdFSM.cs` | Selects flight states and handles activation. |
| `Assets/TEST/BirdMovement.cs` | Applies movement through a `CharacterController`. |
| `Assets/TEST/AnimatorController.cs` | Updates avatar animation parameters. |
| `Assets/TEST/Hand poseshape/` | Hand-pose and hand-shape definitions. |
| `Assets/final_demo/Script/navigator.cs` | Tracks checkpoint progression. |
| `Assets/final_demo/Script/directionUI.cs` | Displays direction, arrival status, and elapsed time. |
| `Assets/final_demo/Scene/` | Bird-flight and teleportation scenes. |

## Team and provenance

Developed by **강수한**, **Inhyuk Song (송인혁)**, and **최승재** for Game Interactive Technology at Kyung Hee University.

This is a snapshot of the original team project, re-hosted by a project member:
[enopid/final_demo](https://github.com/enopid/final_demo), branch `integration`.

Unity packages, sample code, and third-party assets retain their respective credits and license terms.
