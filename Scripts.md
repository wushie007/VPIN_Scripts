# PinupPopper Scripts

VPX Launch PinupPopper Dual Launch Script. This script sets up dual launch for PinUp Popper Video Tables, VR Tables, and tables with original back glass. It includes a separate .ini file to use VPX_GL with all options.

```@echo off
START "" "[STARTDIR]Launch\VPXSTARTER.exe" 30 10 60 "Visual Pinball Player" 2
cd /d "[DIREMU]"

rem LOG must be set AFTER cd to [DIREMU] so relative path works
set "LOG=vpinLaunch.log"
set "ini=[DIRGAME]\[GAMENAME]"
echo ===== %DATE% %TIME% ===== >> "%LOG%"

rem Change the following to EnableTrueFullScreen to default FullScreen Exclusive!
SET FSMODE=DisableTrueFullScreen

Rem SET VPXEXE="VPinballX64.exe"
SET VPXEXE="c:\vPinball\VisualPinball\VPinballX_GL64.exe"

if "[RECMODE]"=="1" (SET FSMODE=DisableTrueFullScreen )
if /I "[CUSTOM1]"=="NOFSX" (SET FSMODE=DisableTrueFullScreen )
if NOT "[ALTEXE]"=="" (SET VPXEXE=[ALTEXE] )
SET ALTPARAM=
if /I "[ALTMODE]"=="NOPUP" (SET ALTPARAM=-c1 NOPUP )
echo [Launch] Made it to altmode >> "%LOG%"
echo [Launch] ini var is %ini% >> "%LOG%"
if /I "[ALTMODE]"=="VR" SET ALTPARAM=-c1 VR
if /I "[ALTMODE]"=="VR" goto DO_VR_SWAP
goto SKIP_VR_SWAP

:DO_VR_SWAP
echo [Launch] Doing VR swap >> "%LOG%"
echo [Debug] Checking %ini%.ini >> "%LOG%"
if exist "%ini%.ini" (
    echo [Debug] Original ini exists, moving to .bak >> "%LOG%"
    move /Y "%ini%.ini" "%ini%.ini.bak"
) else (
    echo [Debug] Original ini NOT found >> "%LOG%"
)
echo [Debug] Checking %ini%.ini.VR >> "%LOG%"
if exist "%ini%.ini.VR" (
    echo [Debug] VR ini exists, moving to .ini >> "%LOG%"
    move /Y "%ini%.ini.VR" "%ini%.ini"
) else (
    echo [Debug] VR ini NOT found >> "%LOG%"
)
if exist "%ini%.ini" (
    echo [Launch] VR swap SUCCESS >> "%LOG%"
) else (
    echo [ERROR] VR swap FAILED - ini not found after move >> "%LOG%"
)
echo [Launch] VR swap complete >> "%LOG%"

:SKIP_VR_SWAP
echo [Launch] Past Alt mode >> "%LOG%"
START /min "" %VPXEXE% -%FSMODE%  -minimized -play "[GAMEFULLNAME]" %ALTPARAM%
if %FSMODE%==DisableTrueFullScreen (START "" "[STARTDIR]Launch\PopperKeepFocus.exe" "Visual Pinball Player" 10)
curl -X POST --data-urlencode "table=[GAMEFULLNAME]" --data-urlencode "emu=[DIREMU]" http://localhost:8089/service/gameLaunch```