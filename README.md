# oeadvscan

[AdvanceScan](https://github.com/amadvance/advancescan) for MAME ROMs managed through [OpenEmu](http://openemu.org).

This is a wrapper for `advscan`. A utility to repair and update MAME rom sets. It was made to simplify its use for OpenEmu. Install it through Homebrew with the following:

    brew install dvessel/oetools/oeadvscan

# usage

    oeadvscan [command] --version=N --save-report

    scan           : Generates a report specific to your collection.
    scan-verbose   : Massive report dump includes everything supported by MAME.
    repair         : Repairs roms/disks/samples.
    repair-preview : Safe preview of changes.

    Or pass in arguments for advscan minus the xml info file.
    Preset text commands and pass-through arguments cannot be combined.
    See 'advscan --help' or 'man advscan'.

    --version=NUMBER can optionally be set to a specific MAME version. Applies
    to all commands including pass-through commands for advscan. The version is
    determined by the MAME core plugin from OpenEmu when not set.

    --save-report will save the output to 'AdvanceScan/reports'.

# more info

ROMs will be treated as a [**split set**, not merged or non-merged sets](https://choccyhobnob.com/demystifying-mame-roms/) and they must be in the form of zip files. If you run it on anything but a split set, it may strip parent dependencies from the set preventing it from running. You will have to add the parent back into your roms folder if this occurs.

A new folder will be created within `~/Library/Application Support/OpenEmu/AdvanceScan`. Your games library must be at their default location for it to work. A `sample` directory will be created if it doesn't exist and it will be soft linked along with the `Arcade` roms folder.

If you have an updated set of ROMs, place them into the `_import` folder. `oeadvscan` will keep your existing library intact. No new games will be added. It will only update what’s already there. Any junk and outdated files will be moved into `_unknown`. There is an option to import new games but it's only possible with arguments being passed through to `advscan`. See `man advscan` for details. They will be placed within the `new` folder.

It's recommended to add new games by manually importing them through OpenEmu then run the scan again when needed. This will keep your library tidy and prevent OpenEmu from losing track of everything.

# limitations and oddities

- Running a verbose scan will misreport a lot of files. Files will be listed as good even though they are missing and vice versa. The script will double check and prefix every file with a `+` when it exists and `-` when it doesn't. This option should probably be removed entirely. Not sure what I was thinking here.
- `advscan` can't handle chd files when it's in a sub-directory. The script does its best to scan for it and force it to read them anyway. They will not be moved around. It will only verify their checksum. If a chd needs to be fixed, you must move a working version manually to the correct folders.
