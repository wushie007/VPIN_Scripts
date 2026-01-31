# VPIN Scripts

A collection of scripts and configuration guides for running Visual Pinball X (VPX) tables with PinUP Popper, including support for VR, cabinet mode, and dual launch configurations.

## Overview

This repository contains launch scripts, configuration examples, and table modification guides to enhance your virtual pinball setup. The scripts enable seamless switching between VR and cabinet modes while managing PinUP Popper integration.

## Contents

### [Scripts.md](Scripts.md)
Launch and close scripts for PinUP Popper integration:
- **VPX Launch Script**: Dual launch configuration with VR table support, automatic .ini file swapping, and custom parameters
- **Close Script**: Properly restores .ini files after gameplay and handles cleanup

**Key Features:**
- Automatic .ini file swapping for VR vs. Cabinet mode
- Support for VPX_GL with custom settings
- Configurable full-screen modes
- Background process management
- Logging for debugging

### [VPXedits.md](VPXedits.md)
Step-by-step guide for modifying VPX table scripts to support dual launch modes:
- ROM-based table modifications using the Controller object
- Non-ROM table modifications using PupPack variables
- Disabling B2S backglass when PupPack is enabled
- Code examples

### [VPX_Ini.md](VPX_Ini.md)
Configuration guide for VPX .ini files:
- Standard .ini settings for cabinet/desktop mode
- VR-specific .ini settings and optimizations
- Graphic settings for optimal VR performance
- Documentation links

## Quick Start

1. Review [Scripts.md](Scripts.md) to set up your launch and close scripts in PinUP Popper
2. Follow [VPXedits.md](VPXedits.md) to modify your table scripts for dual launch support
3. Create custom .ini files using [VPX_Ini.md](VPX_Ini.md) as a guide
4. Configure PinUP Popper to use the launch scripts with appropriate ALTMODE parameters:
   - `VR` - Launch in VR mode
   - `NOPUP` - Launch without PupPack
   - Default - Standard cabinet mode with PupPack

## Notes

- VR table support requires two .ini files per table: standard `.ini` and `.ini.VR`
- If you don't use VR, you can simplify by using the standard dual launch example from the [PinUP Popper documentation](https://www.nailbuster.com/wikipinup/doku.php?id=pinup_optional)

## Credits

Based on dual launch techniques from the PinUP Popper community and optimized for VPX_GL with VR support.

## Support

For more information on VPX .ini settings, see the [VPinball Wiki](https://github.com/dekay/vpinball-wiki/wiki/VPinball-Ini)