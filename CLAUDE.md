# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

KhaosKorps Essentials is a fork of EssentialsX, a comprehensive Minecraft plugin suite for Bukkit/Spigot/Paper servers. It provides 180+ commands for teleportation, economy, user management, chat features, and world management.

**Key specs:**
- Java 8 target, requires JDK 21+ for building
- Supports Minecraft 1.8.8 through 1.21.10
- Uses Gradle with Kotlin DSL for build configuration

## Build Commands

```bash
# Build all modules (outputs to jars/ directory)
./gradlew build

# Build without tests
./gradlew build -x test

# Run test server (note the colon prefix)
./gradlew build :runServer

# Run unit tests
./gradlew test

# Generate Javadocs
./gradlew javadoc
```

## Architecture

### Module Structure

**9 Plugin Modules:**
- `Essentials/` - Core plugin (main functionality, 393 Java files)
- `EssentialsAntiBuild/` - Block protection
- `EssentialsChat/` - Chat formatting
- `EssentialsDiscord/` - Discord integration
- `EssentialsDiscordLink/` - Discord account linking
- `EssentialsGeoIP/` - Geographic IP tracking
- `EssentialsProtect/` - Area protection
- `EssentialsSpawn/` - Spawn management
- `EssentialsXMPP/` - XMPP messaging

**5 Provider Modules (in `providers/`):**
Version abstraction layer for multi-version Minecraft support:
- `BaseProviders/` - Base abstractions
- `PaperProvider/` - Paper-specific optimizations
- `NMSReflectionProvider/` - Reflection-based NMS access
- `1_8Provider/` - Minecraft 1.8 implementations
- `1_12Provider/` - Minecraft 1.12 implementations

### Core Package Layout (`com.earth2me.essentials`)

- `commands/` - Command implementations (100+ commands)
- `config/` - Type-safe configuration system with annotations
- `economy/` - Economy system with Vault integration
- `items/` - Item database and resolution
- `perm/` - Permission handling (integrates with LuckPerms/Vault)
- `signs/` - Sign-based functionality
- `api/` - Public API interfaces

### Key Classes

- `Essentials.java` - Main plugin class, extends `JavaPlugin`, implements `IEssentials`
- `EssentialsCommand` - Abstract base class for all commands
- `User` - Player data wrapper with homes, balance, settings
- `plugin.yml` - Defines all commands and permissions

## Build System

- `build.gradle` - Root configuration (group: `com.khaoskorps.minecraft.essentials`)
- `settings.gradle.kts` - Module definitions and repository configuration
- `build-logic/` - Reusable Gradle conventions (checkstyle, shadow, module setup)

Version is auto-generated as `2.0.0-<git-hash>`.

## Testing

Uses JUnit 5 with MockBukkit for Bukkit API mocking. Tests are in `Essentials/src/test/java/`.

## Dependencies

Core: Kyori Adventure (text), Spongepowered Configurate (YAML config), bStats (metrics)
Server: Paper API, Vault API, LuckPerms API