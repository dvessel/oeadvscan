# oeadvscan
[AdvanceScan](https://github.com/amadvance/advancescan) for [OpenEmu](http://openemu.org) MAME core ROMs.

This is a wrapper for AdvanceScan. A utility to repair and updates MAME rom sets. It was made to simplify its use for OpenEmu. Install it through Homebrew with the following.

Add tap:

    brew tap dvessel/oetools

Install:

    brew install oeadvscan

# usage
    scan           : Generates a report specific to your collection. (default)
    scan-verbose   : Massive report dump includes everything supported by MAME.
    repair         : Repairs roms/disks/samples.
    repair-preview : Safe preview of changes.

    Or pass in arguments for advscan minus the xml info file. Preset text commands and pass-through arguments cannot be combined. See 'advscan --help' or 'man advscan'.

    --version=NUMBER can optionally be set to a specific MAME version. Applies to all commands including pass-through commands for advscan. The version is determined by the MAME core plugin from OpenEmu when not set.

    --save-report will save the output to 'AdvanceScan/reports'.

