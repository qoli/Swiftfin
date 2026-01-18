# Repository Guidelines

## Project Structure & Module Organization
- `Swiftfin/` holds the iOS app (SwiftUI views and platform-specific code).
- `Swiftfin tvOS/` holds the tvOS app views and components.
- `Shared/` contains shared models, services, view models, and UI components.
- `PreferencesView/` is a reusable preferences package used by the apps.
- `Resources/` stores assets (images, SVGs, icons).
- `Translations/` contains `*.lproj` localization files.
- `Documentation/` houses contributor docs; `Scripts/Translations/` holds localization utilities.
- `XcodeConfig/` stores local build configs; `Swiftfin.xcodeproj/` is the Xcode project.

## Build, Test, and Development Commands
- `brew install carthage swiftformat swiftgen` installs required tooling (Xcode 15 expected).
- `carthage update --use-xcframeworks` fetches Carthage dependencies (e.g., VLCKit).
- `open Swiftfin.xcodeproj` and build the `Swiftfin` or `Swiftfin tvOS` schemes.
- CLI build examples:
  - `xcodebuild -scheme "Swiftfin" -destination 'platform=iOS Simulator,name=iPhone 15' build`
  - `xcodebuild -scheme "Swiftfin tvOS" -destination 'platform=tvOS Simulator,name=Apple TV' build`
- `swiftgen` regenerates `Shared/Strings/Strings.swift` from `Translations/en.lproj`.

## Coding Style & Naming Conventions
- SwiftFormat is the formatter/linter; run `swiftformat .` before submitting.
- Indentation is 4 spaces (Xcode indentation), max line width 140.
- Use Swift naming conventions: `UpperCamelCase` for types, `lowerCamelCase` for values/functions.
- Generated files: `Shared/Strings/Strings.swift` is SwiftGen output; do not edit manually.

## Testing Guidelines
- No dedicated XCTest targets are present; rely on simulator builds and manual verification.
- CI expects successful iOS and tvOS builds plus a passing SwiftFormat lint check.

## Commit & Pull Request Guidelines
- Commit messages are short and descriptive; examples include `Fix Fastlane in CI (#1899)`.
- Translation updates are typically auto-committed as `Translated using Weblate (Language)`.
- Follow Jellyfin PR guidelines with clear descriptions, linked issues when relevant, and UI screenshots for visual changes.
- Merge requirements (per `Documentation/contributing.md`): iOS/tvOS builds pass, no developer account attached, SwiftFormat passes, new strings localized, and labels applied when relevant.

## Configuration Tips
- For local signing, create `XcodeConfig/DevelopmentTeam.xcconfig` with:
  ```
  DEVELOPMENT_TEAM = "YOUR_TEAM_ID"
  PRODUCT_BUNDLE_IDENTIFIER = org.jellyfin.swiftfin
  ```
- The file is gitignored; keep credentials out of the repo.
