# Auto-Discovery Service for Shelly Smart Bulbs

## Problem Description

An event production company deploys Shelly Duo GU10 RGBW bulbs at conference venues and art installations. Because venue network infrastructure varies — different routers, different DHCP servers — the team cannot rely on pre-configured IP addresses for each bulb. They need a Kotlin service that automatically finds all Shelly color bulbs on the local network at startup and returns their IP addresses, so the main lighting controller can connect to them without any manual configuration.

The discovery mechanism should use mDNS (multicast DNS), which the Shelly bulbs broadcast on the local network. The team has encountered a known issue when running on macOS laptops during development where discovery returns no results, even though bulbs are present and reachable via their browser. The solution must handle this correctly.

Both the standard Shelly color bulb and the Duo GU10 families should be recognized during discovery.

## Output Specification

Produce the following files:

- `ShellyDiscovery.kt` — a Kotlin file containing a `discoverShelly` function (or equivalent) that performs mDNS discovery and returns a list of IP address strings for all discovered Shelly color bulbs. Include the helper needed to select the correct network interface. Include all necessary imports.
- `build.gradle.kts` — a Gradle build file showing the dependency required for mDNS discovery to work.
