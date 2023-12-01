- `BB_FETCH_PREMIRRORONLY` - only search `PREMIRRORS` for files if enabled.  Skip `SRC_URI` and `MIRRORS`. 
- `BBLAYERS` - List of layers enabled for the build.  Defined in `bblayers.conf`.
- `BBFILES` - List of recipe files BitBake uses to build software.  These are `*.bb` and `*.bbappend` files.
- `BBPATH` - Where to search for `.bbclass` and `.conf` files.
- `LAYERDIR` - Path to current layer.  Only available inside `layer.conf`.
- `PREMIRRORS` - Where to get source code from.  Order is
	1. local download directory
	2. `PREMIRRORS`
	3. upstream source (i.e. `SRC_URI`)
	4. `MIRRORS`
- `TOPDIR` - Bitbake's build directory.

- `BBFILE_PATTERN_${PN}` - regex to specify files for specified, `${PN}`, layer.
- `BBFILE_PRIORITY` - Priority of layer.  HIgher number is higher priority.

- `B` - "Build" directory.  By default, the same as `${S}`
- `BP` - Base recipe name.  Name and version without any special suffixes.  (i.e. `${BPN}-${PV}`)
- `BPN` - "Base `PN`".  `PN` with common prefixes and suffixes removed (e.g. `lib32-`, `-cross`, etc.).
- `D` - Root of "Destination" directory.
- `EXTENDPE` - Usually blank.  Only set if `PE` is set.
- `FILES` - List of files to install.
- `PE` - epoch of recipe.  Usually unset.
- `PN` - Recipe name.
- `PR` - Recipe revision (e.g. "r0", "r1", etc.).
- `PV` - Recipe version (e.g 3.4.2).
- `S` - "Source" directory.  Location of unpacked source for current recipe.  By default, it is `${WORKDIR}/${BPN}-${PV}` which reduces to `${WORKDIR}/${BP}`.
- `WORKDIR` - Working directory where recipe is built. Defined as::
```
  ${TMPDIR}/work/${MULTIMACH_TARGET_SYS}/${PN}/${EXTENDPE}${PV}-${PR}
```
- `IMAGE_CLASSES` - List of classes that all images should inherit.

# Dependencies
- `DEPENDS` - Packages (i.e. recipes) required to build package.  Build-time dependencies.  The `do_configure()` task depends on the `do_populate_sysroot()` task of the specified prerequisite.
- `RDEPENDS` - Runtime dependency for package.  Not required for building.  The `do_build()` task depends on the `do_package_write()` task of the prerequisite.

Dependencies can specify versions.  For example,
- `DEPENDS = "recipe-b (>= 1.2)"`

# Removing Entries

`FOO:remove = "thing-to-remove"` ^[See: https://docs.yoctoproject.org/bitbake/2.2/bitbake-user-manual/bitbake-user-manual-metadata.html#removal-override-style-syntax]

# References
- [Variables Glossary](https://docs.yoctoproject.org/ref-manual/variables.html)
