AirMap-WorldGuard
================

AirMap-WorldGuard adds WorldGuard region overlay support to dynmap.

This is a maintained fork of
[Dynmap-WorldGuard](https://github.com/mikeprimm/Dynmap-WorldGuard) by
mikeprimm. It targets Paper v26.x and builds with Gradle instead of the Maven
build used on the upstream master branch.

This plugin is built against the dynmap marker API 3.8 and detects the map
plugin by the name `dynmap`.
[AirMap](https://github.com/airgalaxie/AirMap) works as well: it provides
itself under the name `dynmap` and implements the same marker API 3.8, so it is
picked up without any special handling and is never queried under its own name.
The Dynmap project itself does not support AirMap, and AirMap is not an
official Dynmap release.

Compatibility
-------------

| Component | Version |
| --- | --- |
| Java bytecode target | 25 |
| Gradle wrapper | 9.8.0 |
| Server API | Spigot/Paper API 26.3-R0.1-SNAPSHOT |
| dynmap API | 3.8 (`dynmap-api` + `DynmapCoreAPI`) |
| WorldEdit Bukkit | 7.4.5 |
| WorldGuard Bukkit | 7.0.19 |
| Shadow plugin | 9.6.1 |

The build must be run with a JDK that can target Java 25. A newer JDK, such as
JDK 26, can also run the build.

Building
--------

Use the included Gradle wrapper:

```sh
./gradlew build
```

The plugin jar is produced by the Shadow plugin under `build/libs/`.

Useful build tasks:

```sh
./gradlew compileJava
./gradlew shadowJar
./gradlew packageZip
./gradlew printJavaCompatibility
```

Project layout
--------------

| Path | Purpose |
| --- | --- |
| `settings.gradle` | Project name `AirMap-WorldGuard`, plugin and dependency repositories |
| `build.gradle` | Java 25 target, compile-only dependencies, Shadow jar and zip packaging |
| `gradle/libs.versions.toml` | Version catalog for all dependencies and the Shadow plugin |
| `src/main/java/org/airmap/worldguard/AirMapWorldGuardPlugin.java` | Plugin entry point |
| `src/main/resources/paper-plugin.yml` | Paper plugin metadata (preferred descriptor) |
| `src/main/resources/plugin.yml` | Legacy Bukkit descriptor, kept as fallback for non-Paper servers |
| `src/main/resources/config.yml` | Default configuration |
| `LICENSE` | Apache License 2.0 |
| `NOTICE` | Attribution for the upstream project and dynmap |

Runtime Dependencies
--------------------

Install this plugin on a Paper v26.x server with dynmap and WorldGuard present.
The Paper plugin metadata declares both as required server dependencies.

The plugin looks up the map plugin by the name `dynmap`, uses the marker set id
`worldguard.markerset` and registers the WorldGuard boolean flag `dynmap-boost`;
all three are kept identical to upstream so existing marker sets and region
flags keep working. Because the plugin name changed to `AirMap-WorldGuard`, the
server keeps its configuration in `plugins/AirMap-WorldGuard/config.yml`; copy
an existing `plugins/Dynmap-WorldGuard/config.yml` over on first start.

Changes compared to upstream master
-----------------------------------

- Renamed the project, artifacts and plugin descriptor to `AirMap-WorldGuard`.
- Moved the plugin package from `org.dynmap.worldguard` to
  `org.airmap.worldguard` and renamed the main class to
  `AirMapWorldGuardPlugin`.
- Replaced the Maven build files with Gradle wrapper files, `settings.gradle`,
  `build.gradle`, and a Gradle version catalog.
- Switched from the Bukkit API dependency to the Spigot/Paper 26.3 API
  (`org.spigotmc:spigot-api:26.3-R0.1-SNAPSHOT`).
- Added Paper's `paper-plugin.yml` metadata with required `dynmap` and
  `WorldGuard` server dependencies.
- Raised the compile target from Java 8 to Java 25.
- Updated dynmap API from `3.3-SNAPSHOT` to `3.8`.
- WorldEdit Bukkit `7.4.5`, WorldGuard Bukkit `7.0.19`.
- Removed bStats usage and the bStats shaded dependency from the plugin.
- Added the Apache License 2.0 and a `NOTICE` file.

License
-------

Licensed under the Apache License, Version 2.0. See `LICENSE` and `NOTICE`.

Thanks to mikeprimm for the original Dynmap-WorldGuard plugin and for dynmap.