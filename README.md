# Drone OSC Controller
Drone OSC Controller adds additional controls to the drone in VRCLens using VRChat OSC.

The most typical setup in VRCLens only allows lateral movement with hand based rotation.
This has the downside of having to twist your hand in awkward positions when attempting to do 360 degree video.
We solve this in VR by passing opposite hand controller data through OSC avatar parameters to control vertical and horizontal pitch.
Additionally, this projects provides Xbox controller OSC for your drone to enable a more comfortable experience and VRChat Desktop supportw.

## Install Drone Controls

Download and import the unity package from the [latest release](https://github.com/qbitzvr/Drone-OSC-Controller/releases/latest).

Installation Video Guide: https://youtu.be/Arz9iQ2-MKo

### Prerequisites:
- Have an avatar with [VRCLens](https://hirabiki.gumroad.com/l/rpnel) already installed.
- Install [Modular Avatar](https://modular-avatar.nadena.dev/) through VRChat Creator Companion.
- Backup your project.

### Full Controller Installation
1. In the `Full Controller` folder, place the `Drone OSC Controller` prefab on your avatar in the Hierarchy window.
2. In the VRC Avatar Descriptor of your avatar, find the FX layer (click on it), duplicate it in the Project tab (ctrl+d), then rename and open the new FX layer.
2. In the Animator window of the new FX layer, delete the following layers:
- `vCNT_DirectStream 224`
- `vCNR_DroneSpeed`
- `vCNP_Drone 212-214 i234`
3. Set the newly created FX layer in your Avatar Descriptor.

## Usage
1. Install the latest release of ThumbParamsOSC: https://github.com/I5UCC/VRCThumbParamsOSC  
For Xbox controls, install the custom build from https://github.com/qbitzvr/VRCThumbParamsOSC/releases/tag/v2.1.0-xbox.0
2. Run `Configurator.exe` to and select the avatar parameters specified in the ExpressionParameters you merged.
3. Run `ThumbParamsOSC.exe` once, this will automatically register it as an overlay in steamvr and [run automatically on startup](https://github.com/I5UCC/VRCThumbParamsOSC#automatic-launch-with-steamvr) 
4. Start VRChat, switch to your avatar, in the Action menu, go to `Options`>`OSC`>`Enable` 

- For VR controllers, open `Move Camera` Puppet Menu main hand, open any action menu on opposite hand to prevent one-handed movement.
- For Xbox controller, wait until xinput update for ThumbParamsOSC (WIP). You will also need to stop vrchat from using the controller as input with HidHide: https://github.com/nefarius/HidHide

### Menu
After install, you will see a new submenu `Drone OSC Controller`.
- `Enable Drone OSC Controller`: Turn on drone OSC controls.
- `Enable Xbox Controller`: Use the Xbox controller instead of VR controller.
- `Drone Direct (Desktop)`: Use DirectCast mode when you move the drone via `Move Camera`. Only effects Desktop mode.
- `Mirror Hand Controls (VR)`: When enabled, uses the left thumbstick for rotation control instead of the right thumbstick. Only effects VR mode.
- `Drone Rotation Speed`: Radial puppet menu that controls the speed of rotation.

## Tweaks
### Make drone motion smoother (highly recommeded)
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

### VR Only Controller or XBox Only Controller Installation
*Deprecated*

Requires [AV3 Manager](https://github.com/VRLabs/Avatars-3.0-Manager) installed through VRChat Creator Companion.

#### Merge FX controller:
1. Navgate to VRLabs/Avatar 3.0 Manager
2. Set Avatar to your avatar.
3. Layers -> FX -> `Add animator to merge`
4. Set Animator = `Drone VR FX` or `Drone Xbox FX` depending on which you would like to use
5. Under parameters, delete all boxes with suffix characters (delete ` 0`)
6. Click `Merge on current`

#### Merge Parameters:
1. On AV3 Manager, go to Parameters tab
2. Under Copy parameters, select `Drone VR ExpressionParameters` or `Drone Xbox ExpressionParameters`
3. Click `Copy parameters`

#### Remove old FX layer:
1. Navigate to your fx layer on your avatar.
2. rename `vCNP_Drone 212-214 i234 0` to `vCNP_Drone 212-214 i234 modified` (just as a reminder)
3. delete `vCNP_Drone 212-214 i234`
