# Custom VPX.ini Scripts
Using the dual launch outlined will require dual .ini files for VR tables and at least a single vpx.ini for each table. 
More information on the .ini file settings can be found at https://github.com/dekay/vpinball-wiki/wiki/VPinball-Ini
These changes will overwrite any normal settings that are set in the GL version. 

Example of .ini for normal launch

Important: If the GL launches for all tables, this option in the ini file will disable VR mode for non-VR play.
**Note:** I set my default graphic settings in VPX GL for non-VR play.

```
[PlayerVR]
AskToTurnOn = 2
```


### VPX.ini.VR File Changes
Copy over the normal .ini file and rename it.
Add in the following changes

```
[PlayerVR]
AskToTurnOn = 0
```
Enables VR mode

```
[Player]
NudgeStrength = 0.00
MaxFramerate = 0
MaxPrerenderedFrames = 0
FXAA = 0
Sharpen = 0
ScaleFXDMD = 0
DisableAO = 0
DynamicAO = 1
SSRefl = 1
PFReflection = 1
MaxTexDimension = 0
AAFactor = 1.000000
MSAASamples = 4
DisableDWM = 0
UseNVidiaAPI = 0
ForceBloomOff = 0
ForceAnisotropicFiltering = 1
CompressTextures = 0
SoftwareVertexProcessing = 0
```
Set custom Graphic settings for VR

