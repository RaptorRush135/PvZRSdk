# 🌱 PvZRSdk

[![NuGet](https://img.shields.io/nuget/v/RaptorRush135.PvZR.Sdk.svg)](https://www.nuget.org/packages/RaptorRush135.PvZR.Sdk)
[![.NET](https://img.shields.io/badge/.NET-6.0-512BD4)](#)
[![License](https://img.shields.io/github/license/RaptorRush135/PvZRSdk.svg)](LICENSE)

> A MSBuild Sdk for creating MelonLoader mods for Plants vs. Zombies™: Replanted.

## Overview

PvZRSdk simplifies the development of MelonLoader mods for PvZ: Replanted by providing automated project setup, version control, deployment, and packaging through an MSBuild SDK.

To get started, see [PvZRModTemplate](https://github.com/RaptorRush135/PvZRModTemplate).

- [Configuration](#%EF%B8%8F-configuration)

- [Version Management](#-version-management)

---

## ✨ Features

### 🎯 Project Defaults
- **.NET 6.0** target framework
- Nullable reference types
- Implicit usings
- Latest C# language version
- x64 platform targeting
- Invariant globalization
- Base EditorConfig

### 🔄 Automatic Versioning
- **[MinVer](https://github.com/adamralph/minver) Integration**: Automatically determines mod version from git tags
- **Manual Override**: Set `ModVersion` property to override auto-detection

### 📝 Auto-Generated ModInfo.cs
- Automatically generates metadata file during compilation
- Contains mod information:
  - **Name**: Derived from RootNamespace
  - **Version**: From `ModVersion` property
  - **Author**: From `ModAuthor` property
  - **DownloadLink**: From `ModDownloadLink` property
- Compiled directly into your DLL for easy access at runtime

### ✅ Build Validation
- Validates `PvzReDir` path exists before compilation
- Ensures MelonLoader is installed in the specified directory

### 🚀 Automatic Deployment
- Copies compiled DLL to `{PvzReDir}\Mods` folder post-build

### 📦 Release Packaging
- **Debug info**: Emits debugging information into the .dll.
- **Release zip**: Creates `.zip` packages automatically
    - **Folder Structure**: Maintains proper `Mods\` hierarchy in zip

### 🩹 Polyfills
- [PolySharp](https://github.com/Sergio0694/PolySharp)
- [Others](https://github.com/RaptorRush135/PvZRSdk/tree/main/src/PvZR.Sdk/Polyfills)

### 🔍 Code Quality Analysis
Integrated code analyzers:
- [NewStyleCop.Analyzers](https://github.com/bjornhellander/NewStyleCopAnalyzers)
- [SonarAnalyzer.CSharp](https://github.com/SonarSource/sonar-dotnet)
- [Roslynator.Analyzers](https://github.com/dotnet/roslynator)

---

## ⚙️ Configuration

### Configurable Properties

| Property                   | Type     | Default Value                                                 | Description                                                                                                                          |
|----------------------------|----------|---------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------|
| `IsModBuild`               | `bool`   | `true`                                                        | Whether to apply mod-specific build targets (deployment, packaging, Melon References & Metadata). Set `false` for library projects.  |
| `PvzReDir`                 | `string` | `C:\Program Files (x86)\Steam\steamapps\common\PVZ Replanted` | Path to PvZ: Replanted installation directory.                                                                                       |
| `ModVersion`               | `string` | *(Auto-detected by MinVer)*                                   | Explicit mod version override. If empty, MinVer automatically determines version from git tags.                                      |
| `ModAuthor`                | `string` | `???`                                                         | Mod creator/author name.                                                                                                             |
| `ModDownloadLink`          | `string` | `TODO`                                                        | Download or repo URL of the mod.                                                                                                     |
| `ModMelonType`             | `string` | *(Required)*                                                  | Fully qualified type name of the mod class that inherits from `MelonMod`.                                                            |
| `ModColor`                 | `string` | *(Optional)*                                                  | Color for the mod in the MelonLoader console. Format: ARGB (e.g., `255, 0, 200, 0`).                                                 |
| `ModZipReplaceVersionDots` | `bool`   | `true`                                                        | Replace dots in version number with dashes in zip filename (e.g., `MyMod1.0.0.zip` → `MyMod1-0-0.zip`).                              |

---

## 📚 Version Management

### Using Git Tags with MinVer

Versions are automatically determined from git tags:

```bash
# Create a version tag
git tag v1.0.0
git push origin v1.0.0

# Build will automatically use version 1.0.0
dotnet build
```

See [MinVer](https://github.com/adamralph/minver) for additional configuration options.

### Manual Version Override

If you need to bypass MinVer:

```xml
<PropertyGroup>
  <ModVersion>1.0.0</ModVersion>
</PropertyGroup>
```
