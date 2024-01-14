# VRCLens OSC Controller

## Install Drone Controls

### Prerequisites:
- Have an avatar with VRCLens already installed.
- Install AV3 Manager through VRChat Creator Companion.
- Backup your project, duplicate your scene and work on that copy.

### Merge FX controller:
1. Navgate to VRLabs/Avatar 3.0 Manager
2. Set Avatar to your avatar.
3. Layers -> FX -> `Add animator to merge`
4. Set Animator = `VRCLens OSC VR Mode FX`
5. Under parameters, delete all boxes with suffix characters (delete ` 0`)
6. Click `Merge on current`

### Merge Parameters:
1. On AV3 Manager, go to Parameters tab
2. Under Copy parameters, select `VRCLens OSC VR ExpressionParameters`
3. Click `Copy parameters`

### Remove old FX layer:
1. Navigate to your fx layer on your avatar.
2. rename `vCNP_Drone 212-214 i234 0" to "vCNP_Drone 212-214 i234 modified` (just as a reminder)
3. delete `vCNP_Drone 212-214 i234`

### Customize controls:
1. Open the FX layer `vCNP_Drone 212-214 i234 modified`
2. Mute the Transitions from `InitDropReset [r]` so only 1 is unmuted to either, `MoveH`, `XInput Controller`, `ThumbParamsOSC`

- `MoveH` - Original behavior
- `ThumbParamsOSC` - Original plus right hand rotation with VR controller (working)
- `XInput Controller` - xbox controller inputs (in development)


# Usage
1. Install ThumbParamsOSC: https://github.com/I5UCC/VRCThumbParamsOSC
2. Run `Configurator.exe` to use avatar parameters specified in `ExpressionParameters vrclens osc`
3. Start VRChat

- For VR controllers, open `Move Camera` Puppet Menu left hand, open any radial menu on right hand.
- For Xbox controller, wait until xinput update for ThumbParamsOSC (WIP). You will also need to stop vrchat from using the controller as input with HidHide: https://github.com/nefarius/HidHide

# Tweaks
## Make drone motion smoother
Reference Video: https://youtu.be/XMcTfFoNUHA?si=sEnlIc5fUIuM7Scj&t=55

In Project Hierarchy:
- `DroneBase` / Parent Constraint / Weight = `0.97`
- `CamObject` / Parent Constraint / Sources / Add `CamObject` Transform
- `CamObject` / Parent Constraint / Sources / Set DroneBase Weight = `0.1`

Animation Changes:
Temporarily set the avatar's base Animator Controller to your FX Controller.

Open Animation Tab, click Preview, scroll dropdown for following animations:
- `DropEnable` - `Parent Constraint.Sources.Array.data[1].weight` = `0.1` (0, 3 seconds)
- `DropHardEnable` - `Parent Constraint.Sources.Array.data[1].weight` = `0.1` (0, 3 seconds)

## Make drone rotation faster
For the following animations, set rotation from `0.1` to `0.2`:
- `RotFastDown`
- `RotFastLeft`
- `RotFastRight`
- `RotFastUp`
