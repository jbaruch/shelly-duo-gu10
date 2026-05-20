# Smart Bulb Controller Library

## Problem Description

A home automation startup is building a mood-lighting platform for boutique hotels. Each room uses Shelly Duo GU10 RGBW smart bulbs connected to the hotel's local WiFi network. The platform needs a Kotlin library to control these bulbs directly over the local network — no cloud service, no third-party hub — because the hotel wants sub-100ms response times for scene transitions and can't tolerate internet-dependency.

The engineering team has confirmed the bulbs expose a local HTTP REST API. They need a clean Kotlin class that wraps this API, covering: setting arbitrary RGB colors with brightness, switching to white light at a specific color temperature, turning the bulb off, and checking whether a bulb is currently reachable on the network. The class should also ensure the bulb is turned off cleanly if the JVM process is killed or exits unexpectedly.

The team is using Kotlin coroutines throughout their stack and prefers coroutine-friendly HTTP clients.

## Output Specification

Produce the following files:

- `ShellyBulb.kt` — the Kotlin class implementing the bulb controller. Include all necessary imports.
- `build.gradle.kts` — a Gradle build file showing the required dependencies for the implementation to compile.

The class should be named `ShellyBulb` and accept the bulb's IP address as a constructor parameter. Use coroutines (`suspend` functions) for all network operations.
