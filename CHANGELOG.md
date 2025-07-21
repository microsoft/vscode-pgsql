# Changelog

Following VS Code guidance, the PostgreSQL extension uses **odd** minor version numbers for
pre-releases and **even** minor version numbers for stable releases.

Read more about pre-release versioning behavior for extensions in the
[VS Code documentation](https://code.visualstudio.com/api/working-with-extensions/publishing-extension#prerelease-extensions).

## [1.7.0] - 2025-07-23

_Pre-release version_

### Added

- SSH connection parameters can now be configured in the Advanced section of the connection dialog. The extension will create an SSH tunnel using the provided credentials, enabling database connections to private networks ([#54](https://github.com/microsoft/vscode-pgsql/issues/54))
- Explicit option for "No Password" authentication type to reduce confusion between missing and intentionally omitted passwords.


### Fixed

- Selecting Entra Authentication type in the Connection String dialog for new connections does not populate default Entra Username or Tenant
- "Script as ..." command on an Object Explorer node with an expired Entra token fails instead of refreshing the token
- New connection attempts that used an incorrect Entra token (from a wrong Entra ID or tenant selection in the UI) will fail even after correcting the settings 
- Connection attempts that fail without error messages are treated as successful by the Object Explorer, but still results in a failed session 
- Unicode characters were incorrectly escaped when embedded in a PostgreSQL array type ([#70](https://github.com/microsoft/vscode-pgsql/issues/70))
- PostgreSQL array values were serialized and displayed as JSON arrays instead of PostgreSQL syntax ([#70](https://github.com/microsoft/vscode-pgsql/issues/70))

### Changed

- When using "Connect with VS Code" from Azure Portal, if the profile already exists, the existing profile dialog opens instead of creating a duplicate. Clicking Connect will now automatically connect using the existing profile. ([#79](https://github.com/microsoft/vscode-pgsql/issues/79), [#38](https://github.com/microsoft/vscode-pgsql/issues/38))


## [1.6.0] - 2025-06-30

Stable release.

This is the stable release of the features introduced in 1.5.0. There are no changes since 1.5.0, but 1.6.0 marks these features as stable for all users.

## [1.5.0] - 2025-06-19

_Pre-release version_

### Added

- Support for selecting Entra Tenant when using Entra ID authentication for PostgreSQL connections ([#17](https://github.com/microsoft/vscode-pgsql/issues/17))
- Support for providing a custom user name or Security Group name when using Entra ID authentication for PostgreSQL connections ([#30](https://github.com/microsoft/vscode-pgsql/issues/30))
- Improved process and thread management for the PostgreSQL Tools Service, including better handling of service restarts and process terminations
- Validate file integrity when downloading PostgreSQL Tools Service archive
- Support for Docker `platform` argument when using custom images for new Docker PostgreSQL creation. This is required for ARM64 architecture support on some images like PostGIS.
- Improved documentation for supported platforms and architectures in the README

### Fixed

- IntelliSense stops working after saving SQL file, or when opening a saved SQL file ([#68](https://github.com/microsoft/vscode-pgsql/issues/68))
- PostgreSQL connection string parsing errors, including issues with underscore characters and connection strings without passwords ([#69](https://github.com/microsoft/vscode-pgsql/issues/69))
- Entra ID token fetching issues and account validation scenarios
- Extension startup crashes caused by invalid or corrupted connection profiles (now validated and ignored on startup)

### Changed

- @pgsql Copilot Chat participant is enabled by default. If GH Copilot Chat is installed, it can be used for chat interactions with your PostgreSQL databases. ([#58](https://github.com/microsoft/vscode-pgsql/issues/58), [#66](https://github.com/microsoft/vscode-pgsql/issues/66))
- Improved layout of command buttons in Query History window

## [1.4.2] - 2025-05-28

### Changed

- Update extension license terms

### Fixed

- Download and extraction errors when installing pgsql tools service archive ([#56](https://github.com/microsoft/vscode-pgsql/issues/56), [#39](https://github.com/microsoft/vscode-pgsql/issues/39), [#13](https://github.com/microsoft/vscode-pgsql/issues/13s))

## [1.4.1] - 2025-05-15

### Fixed

- Broken relative links in bundled README

## [1.3.1] - 2025-05-15

_Pre-release version_

### Fixed

- Update extension metadata for rendering in VS Code Marketplace

## [1.3.0] - 2025-05-14

_Public preview release._

### Added

- Migrate previous `ms-ossdata.vscode-postgresql` extension settings to the new settings on startup

### Fixed

- Handle cases of unexpected EOF streams in the PostgreSQL Tools Service

## [1.2.0] - 2025-05-08

_Initial release to Marketplace for testing public preview._
