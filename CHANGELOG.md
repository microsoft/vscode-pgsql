# Changelog

Following VS Code guidance, the PostgreSQL extension uses **odd** minor version numbers for
pre-releases and **even** minor version numbers for stable releases.

Read more about pre-release versioning behavior for extensions in the
[VS Code documentation](https://code.visualstudio.com/api/working-with-extensions/publishing-extension#prerelease-extensions).

## [1.19.0] - 2026-03-27

### Added

- **Azure HorizonDB Provisioning** — Create and configure Azure HorizonDB clusters directly from the extension, without switching to the Azure Portal.
- **Server Restore / Clone** — Restore or clone Azure Database for PostgreSQL Flexible Server instances from the server dashboard.
- **Deep Object Explorer Refresh** — Refreshing a node in the Object Explorer now performs a deep refresh of its subtree without collapsing the rest of the tree.
- **Apache AGE Graph Visualization Improvements** — Improved layout, controls, and usability of the Apache AGE graph visualization panel.
- **Copilot SQL Auto-Attach** — Added an auto-attach setting to automatically attach SQL context to Copilot conversations. Improved modal prompt and tool guidance for SQL attach workflows. ([#233](https://github.com/microsoft/vscode-pgsql/issues/233))
- **Smarter Query Plan Copilot Recommendations** — Copilot analysis of query plans now uses a verification protocol for more reliable and actionable optimization suggestions. ([#234](https://github.com/microsoft/vscode-pgsql/issues/234))
- **Static Query Plan Summarization** — Query plans can now include static summarization to surface high-level plan characteristics without a full Copilot analysis.
- **Multi-Source Connection Settings** — Connection profiles are now fully settings source-aware. The extension correctly reads from and writes back to the originating settings scope (user, workspace, or folder). Editing a workspace-defined connection no longer silently overwrites global user settings. A scope selector lets you explicitly choose where a new connection profile is saved, and duplicate profiles across scopes are automatically deduplicated. ([#191](https://github.com/microsoft/vscode-pgsql/issues/191), [#133](https://github.com/microsoft/vscode-pgsql/issues/133), [#221](https://github.com/microsoft/vscode-pgsql/issues/221))

### Fixed

- `DROP FUNCTION` script generation produced malformed SQL in some cases ([#236](https://github.com/microsoft/vscode-pgsql/issues/236))
- Foreign tables did not appear in IntelliSense completions ([#197](https://github.com/microsoft/vscode-pgsql/issues/197))
- "Script as Create" on a materialized view always generated the DDL for the first materialized view in the schema, regardless of which object was selected ([#237](https://github.com/microsoft/vscode-pgsql/issues/237))
- `START TRANSACTION` was executed incorrectly, causing unexpected transaction state ([#229](https://github.com/microsoft/vscode-pgsql/issues/229))
- DDL generation for objects using built-in trigger functions (e.g. `tsvector_update_trigger`) produced unquoted arguments ([#227](https://github.com/microsoft/vscode-pgsql/issues/227))
- Exporting query results as JSON double-encoded JSON/JSONB column values ([#235](https://github.com/microsoft/vscode-pgsql/issues/235))
- "Enable richer experiences" command was missing from the Command Palette; disambiguated palette labels for related commands ([#232](https://github.com/microsoft/vscode-pgsql/issues/232))
- Query Plan Visualization search telemetry was inflated due to a counting bug; stabilized Copilot context across plan views
- Schema visualizer legend now uses less vertical screen space
- `pgsql_query_plan` MCP tool `filterType` parameter was not correctly applied in some cases
- Metrics group API validation and pagination handled edge cases incorrectly in some configurations

## [1.18.1, 1.18.2] - 2026-03-15

### Fixed

- [Schema Migrations] Hotfix patches addressing schema migration issues

## [1.18.0] - 2026-02-27

Stable release.

This is the stable release of the features introduced in `1.17.0`. There are no changes since `1.17.0`, but `1.18.0` marks these features as stable for all users.

## [1.17.0] - 2026-02-26

### Added

- **Query Plan Visualization** Explore PostgreSQL EXPLAIN output in four synchronized views: an interactive node graph, icicle chart, sortable table, and raw source. Color-coded severity groups expose performance bottlenecks at a glance, and GitHub Copilot integration provides AI-assisted analysis and optimization suggestions. Launch from the query editor toolbar, the Query Results panel, or the Command Palette. ([read more](README.md#query-plan-visualization))
- **Object Explorer Search** Find database objects by name without expanding the Object Explorer tree. Search across connections, databases, and schemas; filter by object type (tables, views, functions, sequences, and more) or schema name; and click any result to navigate directly to it in the tree. ([read more](README.md#object-explorer-search))
- **Graph Visualization** Apache AGE graph query results are automatically detected and rendered as an interactive node-edge graph directly in the results pane, with per-node callouts, zoom and pan controls, export support, and theme-aware styling. ([read more](README.md#apache-age-graph-visualization))
- **MCP Server** — The extension registers a Model Context Protocol (MCP) server with VS Code, enabling AI assistants to discover and interact with your PostgreSQL databases through a standardized tool interface.
- **Azure Backup Management** — List, create, and delete on-demand backups and configure retention periods for Azure Database for PostgreSQL Flexible Servers directly from VS Code, without switching to the Azure Portal.
- **Azure Server Logs** — Configure log capture settings, set retention periods, and download server and upgrade logs directly from the Server Dashboard for Azure Database for PostgreSQL Flexible Servers.
- [Schema Migrations] Migration service version updated to 2.0.0
- [Schema Migrations] Migration engine now supports GPT5.2 model
- [Schema Migrations] Timeout thresholds for agent conversation and OpenAPI connection
- [Schema Migrations] Object-level conversion now uses JSON-based chunking for more reliable handling of large schemas and cyclic table dependencies.

### Breaking Changes

- The `pgsql_list_servers` Language Model Tool (LMT) has been renamed to `pgsql_list_connection_profiles` to align with the MCP tool name used in templated prompts. Any custom prompts or integrations referencing the old `pgsql_list_servers` tool name must be updated.

### Fixed

- Server parameters multi-select dropdowns now correctly display and match selected values, including case-insensitive comparison against server-returned values
- Docker container creation now validates that a password is provided before starting the container, preventing post-start connection failures
- IntelliSense completions no longer fail to refresh for partitioned tables
- JSON Schema `$ref` resolution warning no longer appears when opening JSON files ([#223](https://github.com/microsoft/vscode-pgsql/issues/223))
- Tool-initiated transactions are rolled back automatically on failure, eliminating the need to manually issue ROLLBACK after a query error ([#166](https://github.com/microsoft/vscode-pgsql/issues/166))

## [1.16.0] - 2026-01-30

Stable release.

This is the stable release of the features introduced in `1.15.0`. There are no changes since `1.15.0`, but `1.16.0` marks these features as stable for all users.

## [1.15.0] - 2026-01-27

### Added

- The extension is now available on Windows 11 ARM64 devices under Prism emulation ([#82](https://github.com/microsoft/vscode-pgsql/issues/82))
- Create new Azure Database for PostgreSQL Flexible Server instances directly from the extension
- Manage Azure Database for PostgreSQL Flexible Server firewall rules, server parameters, and server states directly from the extension
- **Schema filtering** for schema visualization: select specific schemas to include or exclude when visualizing database schemas, accessible from Object Explorer nodes or directly in the visualization tool ([#49](https://github.com/microsoft/vscode-pgsql/issues/49))
- SSL connections now support custom file and "system" `sslrootcert` values, pairing "system" selections with `verify-full` sslmode
- UI elements in Object Explorer and Query Editor will indicate when an active connection is lost
- [Schema Migrations] Additional localization language entries
- [Schema Migrations] Support for Oracle Thick Client Connection
- [Schema Migrations] Best Effort conversion when primary conversion reaches messages limit
- [Schema Migrations] Handle cyclic dependencies in schema objects
- [Schema Migrations] Display success metrics for programmable/non-programmable objects

### Fixed

- Closing query editors returns underlying database connections to the pool for reuse instead of exhausting available connections ([#178](https://github.com/microsoft/vscode-pgsql/issues/178))
- Table results filter panel layout, sizing, and behavior improvements to prevent clipping and improve usability across different panel sizes ([#189](https://github.com/microsoft/vscode-pgsql/issues/189))
- [Schema Migrations] Correctly handle sequence dependencies extraction
- [Schema Migrations] Topological sorting fix in chunking logic to handle cyclic dependencies
- [Schema Migrations] Fix conversion % displayed in report for chunk failures
- [Schema Migrations] Fix connection to Oracle DB using Service ID
- [Schema Migrations] Convert unique indexes as is and not as primary index

## [1.14.0] - 2025-12-17

Stable release.

This is the stable release of the features introduced in `1.13.*`. There are no changes since `1.13.0`, but `1.14.0` marks these features as stable for all users.

## [1.13.0] - 2025-12-15

### Added

- Improved accessibility for Metrics Dashboard with keyboard navigation support for data points and legend controls
- Schema migrations handle appropriate naming of constrains in the coverted DDL statements
- Schema migrations handle conversion of partitions for Oracle to PostgreSQL

### Fixed

- Entra ID authentication now supports Personal Microsoft Accounts (MSA) in addition to work/school accounts ([#183](https://github.com/microsoft/vscode-pgsql/issues/183))
- Connection profiles with duplicate server names, database, and credentials can now be saved, enabling more SSH tunneling and jump host scenarios ([#48](https://github.com/microsoft/vscode-pgsql/issues/48), [#175](https://github.com/microsoft/vscode-pgsql/issues/175))
- Schema migration correctly handle trigger dependencies which caused extraction failures on some schemas

### Changed

- Additional localization language updates

## [1.12.1] - 2025-12-02

### Fixed

- Use new Copilot Chat extension to register @pgsql chat participant, restores "Chat with database" functionality ([#193](https://github.com/microsoft/vscode-pgsql/issues/193))

## [1.12.0] - 2025-11-14

Stable release.

This is the stable release of the features introduced in `1.11.*`. There are no changes since `1.11.4`, but `1.12.0` marks these features as stable for all users.

**Notably, this release makes the Oracle to Azure Database for PostgreSQL migration tooling available for all users in Preview.** This AI-powered feature helps you migrate Oracle database schemas and application code to PostgreSQL. [Learn more](README.md#oracle-to-azure-database-for-postgresql-schema-and-application-conversion-preview).

## [1.11.4] - 2025-11-12

### Added

- [Preview] Oracle to Azure Database for PostgreSQL schema and application conversion ([read more](README.md#oracle-to-azure-database-for-postgresql-schema-and-application-conversion-preview))

### Changed

- macOS arm64 builds no longer require Rosetta 2 emulation

### Fixed

- Prevent corrupt Entra accounts from being saved in connection profiles ([[#164](https://github.com/microsoft/vscode-pgsql/issues/164)])

## [1.11.2, 1.11.3] - 2025-11-06

### Fixed

- Database schema names beginning with `pg` are no longer listed under the "System Schemas" path in Object Explorer

### Changed

- Feedback prompts are not shown when VS Code setting `telemetry.feedback.enabled` is set to `false`

### Added

- Experimental support for Start/Stop/Restart server operations on Azure Database for PostgreSQL Flexible Servers (`pgsql.azureServer.preview.enabled` setting)

## [1.11.0] - 2025-10-16

### Changed

- The extension now includes all platform-specific dependencies and is published per supported platform; no post-install downloads are required. Installs should work for network-restricted environments.
- Updates to improve accessibility and language localization

## [1.10.0] - 2025-10-02

Stable release.

This is the stable release of the features introduced in `1.9.*`. There are no changes since `1.9.1`, but `1.10.0` marks these features as stable for all users.

## [1.9.1] - 2025-10-01

### Fixed

- Stabilize memory consumption in long-running dashboard sessions
- Metric chart x-axis now trims to available data range after user machine sleep or network interruptions
- System metrics normalize rate calculations after user machine wakes from sleep
- Handle Azure API failures during metrics polling

## [1.9.0] - 2025-09-24

### Added

- **Server dashboard** offering high-level metadata plus real-time and historical performance metrics for PostgreSQL servers, providing visibility into server health and workload patterns (historical data available for Azure Database for PostgreSQL Flexible Server). [See more details here](https://aka.ms/pgsql-metrics-feedback).
- **GitHub Copilot Chat integration** for server performance metrics: use natural language to inspect trends, identify bottlenecks, and generate diagnostic SQL.
- Keybinding for "Run Current Statement" in the Query Editor (default: `Ctrl+Shift+Enter`) executes the statement under the cursor without requiring a selection ([#121](https://github.com/microsoft/vscode-pgsql/issues/121), [#103](https://github.com/microsoft/vscode-pgsql/issues/103))
- Dragging an Object Explorer entity into an editor now inserts a correctly double-quoted identifier ([#126](https://github.com/microsoft/vscode-pgsql/issues/126))
- Allow database connections via socket file paths ([#34](https://github.com/microsoft/vscode-pgsql/issues/34))

### Fixed

- Client tools dependency installation is now atomic to prevent partial or corrupted installs ([#144](https://github.com/microsoft/vscode-pgsql/issues/144), [#138](https://github.com/microsoft/vscode-pgsql/issues/138), [#128](https://github.com/microsoft/vscode-pgsql/issues/128))
- "Explain Analyze" toolbar toggle now preserves its correct state for both saved and unsaved SQL files ([#145](https://github.com/microsoft/vscode-pgsql/issues/145))
- Integrated `psql` shell now supports custom binary paths containing spaces on Windows ([#148](https://github.com/microsoft/vscode-pgsql/issues/148))
- Entra auth tokens regenerate when the selected Entra account or tenant changes in the connection dialog
- Removed inadvertent logging of sensitive information in extension logs ([#102](https://github.com/microsoft/vscode-pgsql/issues/102))
- Correct datatype mapping for `oid` values exceeding the Python signed integer limit ([#129](https://github.com/microsoft/vscode-pgsql/issues/129))

### Changed

- Improved connection retry logic and resilience during long-running sessions and transient network interruptions
- Removed deprecated or unused dependencies and upgraded remaining packages

## [1.8.0] - 2025-08-04

Stable release.

This is the stable release of the features introduced in `1.7.*`. There are no changes since `1.7.1`, but `1.8.0` marks these features as stable for all users.

## [1.7.1] - 2025-07-23

### Added

- SSH connection configuration includes ssh-agent support for private key authentication ([#123](https://github.com/microsoft/vscode-pgsql/issues/123))

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
