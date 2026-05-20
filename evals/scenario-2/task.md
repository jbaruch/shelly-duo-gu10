# Real-Time Beat-Synchronized Lighting Controller

## Problem Description

A DJ collective is building a Kotlin application that synchronizes Shelly Duo GU10 RGBW bulbs with live music at their events. An audio analysis pipeline produces color and white/temperature commands at a high rate — sometimes 10–20 updates per second as it tracks beat transients and harmonic content. The controller must forward these commands to the bulb efficiently without flooding the device.

The team's first version used a controller class copy-pasted from an earlier project that drove Govee cloud bulbs at the same venue. With the Govee controller's rate limiting in place, the Shelly feels sluggish: the engineers can see the bulb update perhaps once per second even when the audio pipeline is emitting 15× that. They want the new controller calibrated to what the Shelly hardware actually supports on this network.

A second problem surfaced during last month's event. The DJ ran a long warm-white ambient pre-set, then triggered the RGB beat-chase. The bulb appeared stuck in the previous warm tone for several seconds while the color commands seemed to do nothing, then it snapped over. The team needs the controller to behave correctly when the kind of command being sent changes from one moment to the next.

The application is deployed across multiple venues. The bulb's IP is reserved at each venue's router, but the value differs venue-to-venue. The operator must be able to set the IP for the current venue without rebuilding the app. If they forget, the app should still start up successfully with a sensible default so they can test against the lab bulb during sound-check.

The application runs as a long-lived JVM process. When the process is stopped — Ctrl-C, kill, container shutdown — the bulb must not be left lit.

## Output Specification

Produce the following files:

- `BeatController.kt` — the main Kotlin controller class. It should:
  - Accept color (RGB + gain) and white (temperature + brightness) commands
  - Implement rate limiting calibrated to this hardware's actual responsiveness
  - Correctly handle the case where consecutive commands target different command kinds
  - Register a shutdown behavior so the bulb turns off when the process exits
  - Read the bulb IP from an environment variable
- `build.gradle.kts` — Gradle build file with required dependencies

The rate-limiting interval value should be visible as a named constant or configurable field in the code.
