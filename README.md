AirMap-WorldGuard
================

AirMap-WorldGuard adds WorldGuard region overlay support to dynmap.

This is a maintained fork of
[Dynmap-WorldGuard](https://github.com/mikeprimm/Dynmap-WorldGuard) by
mikeprimm. It targets Paper without encoding a Paper release line in this
README. The exact build and API versions come from
`gradle/libs.versions.toml`.

Map Plugin Detection
--------------------

The plugin is built against the dynmap marker API and detects the map plugin by
the name `dynmap`.
[AirMap](https://github.com/airgalaxie/AirMap) works as well: it provides
itself under the name `dynmap` and implements the same marker API, so it is
picked up without any special handling and is never queried under its own name.
The Dynmap project itself does not support AirMap, and AirMap is not an
official Dynmap release.

Runtime Dependencies
--------------------

Install the plugin on a Paper server with dynmap and WorldGuard present; both
are declared as required server dependencies in
`src/main/resources/paper-plugin.yml`. The legacy `plugin.yml` declares the same
two dependencies for non-Paper servers.

The plugin uses the marker set id `worldguard.markerset` and registers the
WorldGuard boolean flag `dynmap-boost`. Both are kept identical to upstream so
existing marker sets and region flags keep working.

Configuration
-------------

Defaults ship in `src/main/resources/config.yml` and are copied to
`plugins/AirMap-WorldGuard/config.yml` on first start. Because the plugin name
differs from upstream, an existing `plugins/Dynmap-WorldGuard/config.yml` has to
be copied over once.

Keys the plugin reads: `update.period` (seconds between region updates, minimum
15), `layer.name`, `layer.hidebydefault`, `layer.layerprio`, `layer.minzoom`,
`infowindow`, `use3dregions`, `regionstyle.*` (`strokeColor`,
`unownedStrokeColor`, `strokeOpacity`, `strokeWeight`, `fillColor`,
`fillOpacity`, `label`), `visibleregions`, `hiddenregions`, `custstyle.*`,
`ownerstyle.*`, `maxdepth`, `updates-per-tick`.

Building
--------

The included Gradle wrapper builds the plugin:

```sh
./gradlew build
```

Output is written to `target/`:

| Task | Output |
| --- | --- |
| `./gradlew shadowJar` | `target/libs/AirMap-WorldGuard-<version>-<timestamp>.jar`, the jar to deploy |
| `./gradlew packageZip` | `target/libs/AirMap-WorldGuard-<version>-<timestamp>-bin.zip` |
| `./gradlew compileJava` | compiled classes only |
| `./gradlew printJavaCompatibility` | prints the Gradle runtime Java and the compiled bytecode level |

The plugin version and all dependency versions are defined once in
`gradle/libs.versions.toml` (plugin version, Java target, dynmap, WorldEdit,
WorldGuard, Shadow). The Gradle version is fixed by
`gradle/wrapper/gradle-wrapper.properties`. These are build-time values and not
an upper bound: newer dynmap, Paper, WorldEdit and WorldGuard releases, as well
as newer JDKs than the configured bytecode target, are expected to keep working.
The compiled bytecode level is the `javaTarget` entry from the catalog, and the
build runs on any JDK able to target it.

Project layout
--------------

| Path | Purpose |
| --- | --- |
| `settings.gradle` | Project name `AirMap-WorldGuard`, plugin and dependency repositories |
| `build.gradle` | Java target, compile-only dependencies, output directory `target/`, Shadow jar and zip packaging |
| `gradle/libs.versions.toml` | Single source of truth for the plugin version and all dependency versions |
| `gradle/wrapper/` | Pinned Gradle wrapper version |
| `src/main/java/org/airmap/worldguard/AirMapWorldGuardPlugin.java` | Plugin entry point |
| `src/main/resources/paper-plugin.yml` | Paper plugin metadata, preferred descriptor |
| `src/main/resources/plugin.yml` | Legacy Bukkit descriptor for non-Paper servers |
| `src/main/resources/config.yml` | Default configuration |
| `LICENSE` | Apache License 2.0 |
| `NOTICE` | Attribution for the upstream project, dynmap and AirMap |

Changes compared to upstream master
-----------------------------------

- Renamed the project, artifacts and plugin descriptors to `AirMap-WorldGuard`.
- Moved the plugin package from `org.dynmap.worldguard` to
  `org.airmap.worldguard` and renamed the main class to
  `AirMapWorldGuardPlugin`.
- Replaced the Maven build with the Gradle wrapper, `settings.gradle`,
  `build.gradle` and a Gradle version catalog.
- Added Paper's `paper-plugin.yml` metadata with required `dynmap` and
  `WorldGuard` server dependencies, and kept `plugin.yml` for non-Paper
  servers.
- Raised the compile target to the level defined in the version catalog.
- Updated the dynmap marker API from the `3.3-SNAPSHOT` upstream used to the
  version in the catalog.
- Removed bStats usage and the bStats shaded dependency from the plugin.
- Build output moved to `target/`, and plugin version plus all dependency
  versions are read from `gradle/libs.versions.toml`.
- Added the Apache License 2.0 and a `NOTICE` file.

License
-------

Licensed under the Apache License, Version 2.0. See `LICENSE` and `NOTICE`.

Thanks to mikeprimm for the original Dynmap-WorldGuard plugin and for dynmap.