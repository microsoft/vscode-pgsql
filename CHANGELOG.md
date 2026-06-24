# Changelog

Following VS Code guidance, the PostgreSQL extension uses **odd** minor version numbers for
pre-releases and **even** minor version numbers for stable releases.

Read more about pre-release versioning behavior for extensions in the
[VS Code documentation](https://code.visualstudio.com/api/working-with-extensions/publishing-extension#prerelease-extensions).

## [1.25.0] - 2026-06-26

### Added

- **Edit Data** — Edit table rows directly in an editable grid: run the **Edit Data** command from a table’s context menu in Object Explorer, then change cell values, add and delete rows, and save changes back to the database without writing UPDATE/INSERT/DELETE statements by hand. ([#139](https://github.com/microsoft/vscode-pgsql/issues/139))
- **Query Placeholders with Parameter Binding** — Run parameterized queries with typed placeholders and bound parameter values, integrated with the Query Plan Visualizer and an opt-in consent prompt for saving query history. ([#117](https://github.com/microsoft/vscode-pgsql/issues/117))
- **Activity Log in Server Management** — A new Activity Log pane in the server dashboard surfaces Azure control-plane operations for your server directly inside the extension.

### Fixed

- The query results tab now stays where you put it: re-running a query no longer forces the results pane back to the right of the editor, preserving a user-repositioned layout. ([#266](https://github.com/microsoft/vscode-pgsql/issues/266))
- The Schema Designer header colors now meet WCAG AA contrast requirements. ([#269](https://github.com/microsoft/vscode-pgsql/issues/269))
- The connection dialog no longer gets stuck in a stale-selection loop when browsing Azure resources.
- Oracle-to-PostgreSQL migration projects now use the correct settings paths for multi-schema conversions.
- Viewing a database schema no longer crashes when the server has `standard_conforming_strings` turned off. ([#267](https://github.com/microsoft/vscode-pgsql/issues/267))

## [1.24.0] - 2026-06-01

Stable release.

This is the stable release of the features introduced in `1.23.*`. There are no changes since `1.23.6`, but `1.24.0` marks these features as stable for all users.

## [1.23.0 - 1.23.6] - 2026-05-26

### Added

- **AWS RDS IAM Authentication** — Connect to Amazon RDS and Aurora PostgreSQL databases using AWS RDS IAM credentials, with AWS profile and region support plus automatic credential refresh before signed tokens expire. ([#211](https://github.com/microsoft/vscode-pgsql/issues/211), [#219](https://github.com/microsoft/vscode-pgsql/issues/219))
- **Visualize Durable Workflows and AI Pipelines** - (Preview) Support run and definition visualizations for `pg_durable` and `azure_ai.pipelines` created workflows. See the steps, failures, and timings.
- **Horizon DB Network Settings** — Open Horizon DB network configuration from the server dashboard to manage firewall access from within the extension.
- **HorizonDB Azure browse and metadata support** — Browse HorizonDB clusters from the Azure connection flow. Allow fetching Azure metadata for manually entered HorizonDB hosts so dashboard Azure-management features recognize those connections.
- **Agent Mode Database Tools** — The bundled tools service now exposes additional DBAgent MCP tools through the PostgreSQL MCP server, giving AI assistants richer database-analysis and instruction-management capabilities.
- **[Schema Migrations]** — The migration setup experience now includes GA-ready UI updates, Azure Database for PostgreSQL scratch database wording, Microsoft Foundry model configuration labels, and restored enhanced-conversion engine controls.
- **[Schema Migrations]** — The scratch database step can verify recommended Azure Database for PostgreSQL extensions and show any missing extensions inline before schema conversion starts.

### Changed

- Removed AI Model Management interface from HorizonDB provisioning. Will re-enable when it enters Public Preview stage.

### Fixed

- The integrated `psql` terminal command now works when PostgreSQL reports a two-part server version such as `18.3`, instead of failing with an `Invalid Version` error.
- Deep Object Explorer refresh now recovers after dropped schemas and deleted objects instead of leaving stale nodes or failing during refresh. ([#250](https://github.com/microsoft/vscode-pgsql/issues/250))
- The server dashboard now probes `pg_stat_statements` correctly on autocommit connections, avoiding false warnings that the extension could not query an installed extension. ([#259](https://github.com/microsoft/vscode-pgsql/issues/259))
- Connection timeout failures now show clearer, consistent guidance across the connection dialog, Object Explorer, and post-connect notifications.
- Horizon DB creation failures now distinguish total deployment failures from partial follow-up failures, with raw Azure deployment details available for troubleshooting.
- Dashboard AI actions now use the correct Copilot or AI wording and launch chat correctly in Cursor.
- Saved Query History entries can now execute after the original query editor has been closed.
- Server-management actions are now gated by Azure PostgreSQL platform so unsupported management surfaces are not shown for the wrong server type.
- **[Schema Migrations]** — Oracle to Azure Database for PostgreSQL migration tooling is now generally available.
- **[Schema Migrations]** — Refined project layout, provides easier understanding and navigation
- **[Schema Migrations]** — Improvements in object conversion quality and more detailed reporting.
- **[Schema Migrations]** Scratch database extension verification now handles databases where none of the recommended extensions are installed, and changing the PostgreSQL connection no longer triggers stale verification against the previous database.
- **[Schema Migrations]** Review task pending badges and focus indicators now meet accessibility contrast requirements.

## [1.22.0] - 2026-05-08

Stable release.

This is the stable release of the features introduced in `1.21.*`. There are no changes since `1.21.2`, but `1.22.0` marks these features as stable for all users.

## [1.21.0, 1.21.1, 1.21.2] - 2026-05-05

### Added

- **Performance Dashboard** — Investigate database performance from the Server Dashboard with DB load charts, query activity, wait-event analysis, session health, blocking chains, shared time controls, and Azure-aware metrics.
- **Object Properties** — Inspect DDL and security details, including grants and row-level security policies, across all database object types from Object Explorer.
- **Schema-Aware "New Query"** — Right-click a schema in Object Explorer to open a new query with the appropriate `search_path` already set, so unqualified object references resolve inside that schema without manual setup.
([#238](https://github.com/microsoft/vscode-pgsql/issues/238))
- **PostgreSQL Query Plan Node Icons** — The Query Plan Visualizer now uses PostgreSQL-specific node-type icons across all views (graph, icicle, table, and source) so scan, join, and aggregate nodes are easier to identify at a glance.
- **Editor Coordination with the MSSQL Extension** — When both the PostgreSQL and MSSQL extensions are installed, editor ownership is now negotiated between the two, reducing duplicate toolbar actions and conflicting query execution behavior in shared editors.
([#20](https://github.com/microsoft/vscode-pgsql/issues/20), [#67](https://github.com/microsoft/vscode-pgsql/issues/67), [#118](https://github.com/microsoft/vscode-pgsql/issues/118), [#147](https://github.com/microsoft/vscode-pgsql/issues/147))
- **IntelliSense Respects `search_path`** — Completions now honor the `search_path` supplied in connection options, so unqualified names suggest objects from the expected schemas first.
- **Horizon AI Model Management** — Enable AI Model Management when creating Horizon DB resources.
- **[Schema Migrations]** — New enhanced conversion engine offering better DDL conversions at lesser cost & lesser time.
- **[Schema Migrations]** — Dynamic adaptability of conversion speed based on LLM model TPM quota.
- **[Schema Migrations]** — Condensed view of post-conversion "Review tasks" using grouping & categorization to reduce manual effort.

### Changed

- The `@pgsql` chat participant is no longer automatically prompted by product entry points and is planned for future deprecation in favor of Agent Mode and MCP tools.

### Fixed

- Object scripting for partitioned tables now emits the correct `PARTITION BY` clause and partition definitions instead of falling back to the default storage form. ([#27](https://github.com/microsoft/vscode-pgsql/issues/27))
- `Script as Create` now includes generated column definitions such as `GENERATED ALWAYS AS (...) STORED`. ([#248](https://github.com/microsoft/vscode-pgsql/issues/248))
- Deep refresh now recovers when the selected Object Explorer item has already been deleted, instead of failing with an index error. ([#250](https://github.com/microsoft/vscode-pgsql/issues/250))
- Query execution now works for SQL files whose paths contain spaces, percent signs, brackets, backticks, or encoded path segments.
- Fixed a hang during Docker container creation caused by a task-wrapper race condition. ([#252](https://github.com/microsoft/vscode-pgsql/issues/252))

## [1.20.1] - 2026-05-05

### Fixed

- "Analyze with Copilot" from Dashboard Metrics now passes the correct context to the tool, resolving errors that previously occurred during execution.

## [1.20.0] - 2026-03-31

Stable release.

This is the stable release of the features introduced in `1.19.0`. There are no changes since `1.19.0`, but `1.20.0` marks these features as stable for all users.

## [1.19.0, 1.19.1] - 2026-03-27

### Added

- **Azure HorizonDB Provisioning** — Create and configure Azure HorizonDB clusters directly from the extension, without switching to the Azure Portal. HorizonDB is currently in Private Preview, learn more [here](https://azure.microsoft.com/en-us/products/horizondb).
- **Server Restore / Clone** — Restore or clone Azure Database for PostgreSQL Flexible Server instances directly from the server dashboard. Choose a full backup or a specific point-in-time to recover from, and spin up a new server without leaving VS Code.
- **Improved Object Explorer Refresh** — Refreshing a node now reliably picks up all additions and removals throughout its entire subtree, so new database objects appear and deleted ones disappear without needing to disconnect and reconnect. ([#64](https://github.com/microsoft/vscode-pgsql/issues/64), [#152](https://github.com/microsoft/vscode-pgsql/issues/152), [#199](https://github.com/microsoft/vscode-pgsql/issues/199))
- **Multi-Source Connection Settings** — Connection profiles can now be saved to your user settings, workspace, or folder. Save a profile to your workspace settings to check it into source control alongside your code — giving every team member the right database connections whenever they open the project. A scope selector makes it clear where each new profile will be saved, and duplicate profiles across scopes are automatically removed. ([#191](https://github.com/microsoft/vscode-pgsql/issues/191), [#133](https://github.com/microsoft/vscode-pgsql/issues/133), [#221](https://github.com/microsoft/vscode-pgsql/issues/221))
- **Apache AGE Graph Visualization Improvements** — Improved layout, controls, and usability of the Apache AGE graph visualization panel.
- **Copilot SQL Auto-Attach** — Added an auto-attach setting to automatically attach SQL context to Copilot conversations. Improved modal prompt and tool guidance for SQL attach workflows. ([#233](https://github.com/microsoft/vscode-pgsql/issues/233))
- **Smarter Query Plan Copilot Recommendations** — Copilot analysis of query plans now uses a verification protocol for more reliable and actionable optimization suggestions. ([#234](https://github.com/microsoft/vscode-pgsql/issues/234))
- **Static Query Plan Summarization** — Query plans can now include static summarization to surface high-level plan characteristics without a full Copilot analysis.
- [Schema Migrations] Support for Microsoft Entra Authentication for Azure OpenAI Endpoint.

### Fixed

- `DROP FUNCTION` script generation produced malformed SQL in some cases ([#236](https://github.com/microsoft/vscode-pgsql/issues/236))
- Foreign tables did not appear in IntelliSense completions ([#197](https://github.com/microsoft/vscode-pgsql/issues/197))
- "Script as Create" on a materialized view always generated the DDL for the first materialized view in the schema, regardless of which object was selected ([#237](https://github.com/microsoft/vscode-pgsql/issues/237))
- `START TRANSACTION` was executed incorrectly, causing unexpected transaction state ([#229](https://github.com/microsoft/vscode-pgsql/issues/229))
- DDL generation for objects using built-in trigger functions (e.g. `tsvector_update_trigger`) produced unquoted arguments ([#227](https://github.com/microsoft/vscode-pgsql/issues/227))
- Exporting query results as JSON double-encoded JSON/JSONB column values ([#235](https://github.com/microsoft/vscode-pgsql/issues/235))
- "Enable richer experiences" command was missing from the Command Palette; disambiguated palette labels for related commands ([#232](https://github.com/microsoft/vscode-pgsql/issues/232))
- `pgsql_query_plan` MCP tool `filterType` parameter was not correctly applied in some cases ([233](https://github.com/microsoft/vscode-pgsql/issues/233))
- Connecting via a SQL file before opening the PostgreSQL panel could leave Object Explorer showing only the active server; saved connections are now correctly restored in this path ([#242](https://github.com/microsoft/vscode-pgsql/issues/242))
- Schema visualizer legend now uses less vertical screen space


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
