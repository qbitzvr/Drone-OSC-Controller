# Drone OSC Controller
Drone OSC Controller adds additional controls to the drone in VRCLens using VRChat OSC.

The most typical setup in VRCLens only allows lateral movement with hand based rotation.
This has the downside of having to twist your hand in awkward positions when attempting to do 360 degree video.
We solve this in VR by passing right hand controller data through OSC avatar parameters to control vertical and horizontal pitch.
Additionally, this projects provides Xbox controller OSC for your drone to enable a more comfortable experience and VRChat Desktop support (WIP).

## Install Drone Controls

### Prerequisites:
- Have an avatar with [VRCLens](https://hirabiki.gumroad.com/l/rpnel) already installed.
- Install [AV3 Manager](https://github.com/VRLabs/Avatars-3.0-Manager) through VRChat Creator Companion.
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
2. Run `Configurator.exe` to and select the avatar parameters specified in the ExpressionParameters you merged.
3. Run `ThumbParamsOSC.exe` once, this will automatically register it as an overlay in steamvr and [run automatically on startup](https://github.com/I5UCC/VRCThumbParamsOSC#automatic-launch-with-steamvr) 
4. Start VRChat, switch to your avatar, in the Action menu, go to `Options`>`OSC`>`Enable` 

- For VR controllers, open `Move Camera` Puppet Menu left hand, open any radial menu on right hand.
- For Xbox controller, wait until xinput update for ThumbParamsOSC (WIP). You will also need to stop vrchat from using the controller as input with HidHide: https://github.com/nefarius/HidHide

# Tweaks
## Make drone motion smoother (highly recommeded)
Reference Video: https://youtu.be/XMcTfFoNUHA?si=sEnlIc5fUIuM7Scj&t=55

In Project Hierarchy:
- `DroneBase` / Parent Constraint / Weight = `0.97` (smooth), `0.99` (more smooth)
- `CamObject` / Parent Constraint / Sources / Add `CamObject` Transform
- `CamObject` / Parent Constraint / Sources / Set DroneBase Weight = `0.1`

Animation Changes:
Temporarily set the avatar's base Animator Controller to your FX Controller.

Open Animation Tab, click Preview, scroll dropdown for following animations:
- `DropEnable` - `Parent Constraint.Sources.Array.data[1].weight` = `0.1` (0, 3 seconds)
- `DropHardEnable` - `Parent Constraint.Sources.Array.data[1].weight` = `0.1` (0, 3 seconds)

## Change drone rotation speed (optional)
By default, I provide different speed settings in the `Animations` folder, but here's how you can achieve the same effect with the default drone animations.
Replace the rotation magnitude of `0.1` with whatever you like in the following animations.
By default it is `0.4` for VR mode and `0.2` for Xbox controller.
- `RotFastDown`
- `RotFastLeft`
- `RotFastRight`
- `RotFastUp`
