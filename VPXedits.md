# Changes need to the VPX file

### If the VPX table use a rom and controller feature is availble. 
Add the following into the VPX table Script. 
```		If GetCustomParam(1) = "VR" Then
			.PuPHide = 1
		ElseIf GetCustomParam(1) = "NOPUP" Then
			.PuPHide = 1
		ElseCo
			.LaunchBackglass = 0
		End If
```
Example VPX Table Script (used AC DC in this example)
```Sub ACDC_Init
	vpmInit Me
    With Controller
        .GameName = cGameName
		'.Games(cGameName).Settings.Value("rol") = 1
		'.Games(cGameName).Settings.Value("dmd_width")=128
		'.Games(cGameName).Settings.Value("dmd_height")=512
        .SplashInfoLine = "AC/DC LUCI (Stern 2013)"
        .HandleKeyboard = 0
        .ShowTitle = 0
        .ShowDMDOnly = 1
        .ShowFrame = 0
        If NOT CustomDMD Then .Hidden = DesktopMode				'hides the external DMD when in desktop mode and color ROM is not in use
        .HandleMechanics = 0
		If GetCustomParam(1) = "VR" Then   'Lines added Started Custom Options
			.PuPHide = 1
		ElseIf GetCustomParam(1) = "NOPUP" Then
			.PuPHide = 1
		ElseCo
			.LaunchBackglass = 0
		End If  'Lines Added End Custom Options
		On Error Resume Next
        .Run GetPlayerHWnd
        If Err Then MsgBox Err.Description
        On Error Goto 0
    End With
``
### Options if the Table does not have a Rom. 
This can be Tricker. This is my solution for the goonies table Similar tables should have a similar solution. 
Hear I am am using the built functions in the table "enablePupPack, enablePupDMD" and creating a sub function to control them. Bascily we are looking for the Variable that used to control the PUP or reading for the pup pack. Other tables my Simple user usePUP Variable. We would just set Variable in Script which would look a bit diffrently.You Add this in Place of the Variable 

```Dim enablePupPack, enablePupDMD
If GetCustomParam(1) = "VR" Then
	enablePupPack = False
	enablePupDMD = False ' Enable PupPack must be true if this is set to true
ElseIf GetCustomParam(1) = "NOPUP" Then
	enablePupPack = False
	enablePupDMD = False
Else
	enablePupPack = True  ' Enable PupPack DMD and sounds
	enablePupDMD = True  ' Enable PupPack DMD
End If
```

For usePUP Variable
Remove line   usePUP   = True               ' enable Pinup Player functions for this table

```Dim usePUP
If GetCustomParam(1) = "VR" Then
	usePUP = False
ElseIf GetCustomParam(1) = "NOPUP" Then
	usePUP = False
Else
	UsePUP = True  ' Enable PupPack DMD and sounds
End If
```

Right after those changes are made we need to Disable to Backlgass. 

**Note:** The key variable here is `enablePupPack` (or `usePUP` for tables using that variable) which controls the PupPack state.

```
' Disable B2S Backglass if PupPack is enabled
If enablePupPack Then
	On Error Resume Next
	Dim Controller
	Set Controller = CreateObject("B2S.Server")
	Controller.LaunchBackglass = 0
	Controller.B2SSetData 1, 0
	Controller.Run GetPlayerHWnd
	On Error Goto 0
End If
```