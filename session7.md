# <a name="Coding"></a>Pose Tracking 


## Configuring Touchdesigner 

To make the Pose Tracking work, first make sure that the Touchdesigner file from Session 6 is open and running. Then click on the media pipe node and turn on the pose tracking: 
![](images/touchdesignersetting1.jpeg)

Now you should see in the Pose Tracking node that your Pose is being tracked: 
![](images/touchdesignersetting2.jpeg)

## Installing the Light Mover Example

![](images/LightMover.jpeg)

1. Download the following file: [Example Scenes](https://juliannetzer.de/downloads/260615_PoseExamples.zip)

2. Start Unity with the project from Session 6. Extract the zip-file and double click on the LightMover.unitypackage-file, this should open Unity with an Import Dialog. Select everything and click on import. 

3. Click on the LightMover Scene in the Unity Project Window, this should open the example Scene. 

## Understanding the example scene

The scene has two key GameObjects:

- *PoseVisualizer* runs MediaPipePoseVisualizer.cs, which receives body tracking data from MediaPipe via OSC and displays a live skeleton overlay in the corner of the screen.

- *Sphere* runs ArmGestureController.cs, which reads the pose data and moves the sphere based on arm gestures — when both arms point in the same direction (left, right, up, or down), the sphere moves accordingly. Movement speed scales with how far the arms are stretched.

The two scripts are connected: ArmGestureController reads the landmark positions and visibility flags that MediaPipePoseVisualizer continuously updates from the OSC stream.

### MediaPipePoseVisualizer

The `MediaPipePoseVisualizer` is a general-purpose component for receiving and
visualizing MediaPipe pose tracking data in Unity via OSC. It is designed to be
the foundation for any project that uses body tracking — students can use it as
a starting point and build their own gesture logic on top of it.

It exposes two public arrays that other scripts can read:
- `Positions` — the 3D coordinates of all 33 body landmarks
- `ActiveLandmarks` — which landmarks are currently being received

**OSC Settings**
- `Port` — UDP port to receive MediaPipe data on (default: 9000)

**Window**
- `Window Size` — width/height of the skeleton overlay panel
- `Window Margin` — distance from the screen edge
- `Padding` — inner spacing around the skeleton

**Visualization**
- `Dot Size` — size of the joint dots
- `Bone Width` — thickness of the skeleton lines

**Visibility**
- `Visibility Threshold` — how confident MediaPipe must be before a landmark
  is shown (0–1); occluded landmarks fall back to their last known position
- `Occluded Color` — color used for joints and bones that are currently occluded

---

### ArmGestureController

The `ArmGestureController` is an example of how to build custom gesture logic
on top of the `MediaPipePoseVisualizer`. It shows the basic pattern students
should follow in their own projects:

1. Get a reference to the `MediaPipePoseVisualizer`
2. Check which landmarks are active using `ActiveLandmarks`
3. Read the relevant positions from `Positions`
4. Use the data to drive any behavior — movement, animation, interaction, etc.

In this example, the script reads the shoulder and wrist positions of both arms,
detects whether they point in the same direction, and moves the sphere accordingly.

**References**
- `Pose Visualizer` — drag the PoseVisualizer GameObject here (auto-detected if left empty)

**Movement**
- `Move Speed` — overall speed of the sphere

**Gesture Tuning**
- `Min Stretch` — minimum wrist-to-shoulder distance before a gesture is recognized;
  prevents accidental movement when arms are at rest
- `Direction Agreement` — how closely both arms must point in the same direction (0–1);
  lower values are more lenient, 0.3 is a good starting point
- `Smoothing` — how quickly the sphere reacts to gesture changes;
  higher values feel snappier, lower values feel floatier

