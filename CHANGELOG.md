# Changelog

## 1.2.5

- Polished the **Edit Vendit** identity row so the **Name** field receives substantially more horizontal room while the trigger **ID** remains at its practical 240 px width.
- Removed the conflicting inline label width/flex styles that were preventing the identity row from using the available dialog width.
- Kept responsive behavior intact: at narrow widths the Name and ID fields stack cleanly instead of compressing.
- No changes to Vendit data, IDs, inventory, pricing, Tile bindings, proximity, CitiNet, dynamic stock, or Simple Calendar behavior.

## 1.2.4

- Replaced CitiNet sale-card remote **OPEN** behavior with **PING LOCATION** so advertisements can reveal where a sale is without allowing players to shop from across the map.
- Sale pings now animate the viewer to the bound Vendit Tile and use Foundry's native map ping on the active Scene.
- Historical v1.1/v1.2 CitiNet cards that still contain an `OPEN` button are intercepted as location pings after upgrade instead of reopening the shop remotely.
- Added player proximity validation for Tile-bound Vendits. Players must be within **2 grid spaces by default** before the Vendit UI opens; GMs retain unrestricted Preview access.
- Added **Player Interaction Range (grid spaces)** to Vendit Options so the default 2-space range can be adjusted without editing Monk's Active Tiles actions.
- Proximity uses Foundry v12 grid path measurement when available, with a pixel/grid-size fallback for gridless or unsupported measurements.
- The generated Vendit™ Binder already forwards Tile and Token context, so existing bound Tiles automatically gain the proximity gate without adding MATT Distance actions manually.
- Fixed the internal runtime version constant still reporting `1.2.0` in later 1.2.x packages; module/API/runtime now consistently report **1.2.4**.

## 1.2.3

- Replaced the generated **Vendit™ Binder** macro's generic `icons/svg/item-bag.svg` icon with the bundled `assets/Vendit.webp` artwork.
- Existing module-generated Binder macros automatically adopt the new Vendit icon on startup.
- Binder repair now also restores the canonical icon, script type, scope, command, and generated-Binder flag when explicitly requested.
- Added a safety check so an unrelated/custom macro that only happens to share the `Vendit™ Binder` name is not silently rewritten during normal startup.
- No Vendit database, shop, pricing, Tile, Simple Calendar, or CitiNet behavior changes.

## 1.2.2

- Fixed the Dynamic Vendit action bar allowing **Set/Clear Auto-Tile Template** text to bleed outside its button at narrower dialog widths.
- Increased the action grid's minimum cell width so five wide controls no longer get crammed into one row when the dialog cannot comfortably contain them.
- Action buttons now use contained multiline labels with consistent height, centered text, and safe word wrapping.
- No database, Tile binding, dynamic stock, pricing, Simple Calendar, or CitiNet behavior changes.

## 1.2.1

- Fixed the split-second grey Foundry fallback flash when closing Vendit dialogs.
- Fixed product/item images briefly expanding to their natural dimensions while Preview, Edit Vendit, Dynamic Vendit, Manager, Options, or Dynamic Network windows were closing.
- Vendit now hides the application inline before Foundry's close animation and defers removal of its scoped stylesheet/host class until the window is gone.
- Centralized dialog close cleanup so future Vendit windows use the same lifecycle-safe behavior.

## 1.2.0

- Rebuilt Vendit dialog styling into a dedicated retail-terminal skin inspired by the approved dark/cyan/yellow 2077 visual language while keeping Vendit distinct from Choom Trade.
- Added a matching 2045 redline/amber variant using the established `#E64539` era accent.
- Reworked the player shop into a Vendit machine interface with clearer product rows, stock, price, and live-price badges.
- Reflowed Manager, Editor, Dynamic Config, Dynamic Network, and Options layouts to stop long names and controls from overlapping.
- Fixed select/dropdown menus inheriting bright host-theme option backgrounds.
- Gave editor dialogs independent DOM/CSS scopes instead of reusing the Manager body ID.
- Added automatic creation of a **Vendit™ Binder** Monk's Active Tiles helper macro plus Create/Repair controls.
- Added explicit Auto-Tile Template removal in both Dynamic Config and Dynamic Network.
- Clarified that Auto-Tile templates are configuration blueprints; fresh auto-created Vendits no longer copy the template machine's live inventory or timer history.
- Added best-effort rollback if automatic Tile provisioning fails midway, reducing orphaned Vendit records/flags.
- Rebinding a Vendit now clears its old direct Tile flag and repairs stale reverse bindings when possible.
- Deleting a Vendit clears its direct Tile flag and removes any Auto-Tile Template reference.
- Changing a bound Vendit's ID now updates the Tile flag and template reference.
- Added immediate Buy-button locking plus a serialized GM-authoritative purchase path, preventing two players from both buying the final unit.
- Added rollback/refund handling if Item delivery or stock persistence fails during a purchase.
- Restricted authoritative purchase handling to Foundry's active GM so multiple connected GMs cannot double-process one purchase.
- Made purchase chat creation non-critical: a chat-render failure no longer reports a completed dispense as failed.
- Blocked duplicate Vendit IDs in the editor before they can overwrite another machine.
- Kept CitiNet chat card markup and active-Scene-only notification logic unchanged.

## 1.1.2

- Restricted automatic CitiNet sale notifications to Foundry's globally **active Scene** rather than the Scene a GM is merely viewing.
- Added a final active-Scene safety check immediately before creating the public chat message.
- Suppressed due alarms cleanly when no active Scene has an eligible Vendit, preventing delayed catch-up spam.
- Updated manual CitiNet test controls to require the Vendit's Scene to be active.
- Renamed the network test control to **Send Active Scene Test Ping**.

## 1.1.1

- Fixed world-default RollTable and Item compendium references not being inherited by dynamic Vendits.
- Added support for multiple RollTable UUIDs/names and multiple Item pack keys separated by commas, semicolons, or new lines.
- Added robust Foundry v12 TableResult resolution for world and compendium Items, nested RollTables, document links, and direct UUID links.
- Changed dynamic table generation to roll reset clones so Vendit does not consume or exhaust the GM's source RollTables.
- Added a Compendium Pack stock-generator source and made configured pack keys constrain Quick Add suggestions and lookup.
- Added Options buttons to validate configured Item packs and preview configured RollTables.
- Fixed oversized remove buttons and restored usable item-name space in the Dynamic configuration lists.
- Rebuilt CitiNet cards with a responsive grid and a full-width OPEN button so chat text no longer collapses into a vertical column.

## 1.1.0

- Moved the GM launcher to Token Controls to match the Bodega™ Manager workflow.
- Added a Dynamic Network UI and per-Vendit dynamic configuration.
- Added RollTable or curated-list stock generation with configurable 3–6 product defaults.
- Added 2–3 day Simple Calendar stock cycles, background NPC demand, restocking, and skipped-time catch-up.
- Added weighted dynamic pricing from 75–115% of the Item market price, with 100% most common and discounts rare.
- Added scene-local CitiNet flash-price messages using separate curated RollTables or Item lists.
- Added randomized daily CitiNet alarm schedules and collapsed missed alarms to prevent chat spam.
- Added Tile flags, selected-Tile binding, automatic keyword-based Tile creation, and reusable Auto-Tile templates.
- Added a revised Monk’s Active Tiles helper that passes the triggering Tile document, while retaining `id=YOUR-ID` compatibility.
- Added `game.venditrun`, `globalThis.Vendit`, dynamic API methods, and manual processing utilities.
- Migrated existing Items with non-compounding base and regular price references.

## 1.0.1

- Fixed the manager, options, editor, and shop dialogs failing because their per-dialog `bodyId` was not passed into shared CSS and autosize helpers.
- Kept dialog styling isolated while preserving the original Vendit™ UI and database.

## 1.0.0

- Converted Vendit™ Manager macro v3.0.3 into a Foundry VTT v12 ES module.
- Preserved the existing `vendit.db` world setting for automatic data continuity.
- Moved settings registration to the `init` hook and socket binding/API exposure to `ready`.
- Added a GM scene-control launcher.
- Added `game.vendit` public API and legacy-style argument parsing.
- Made scene detection dynamic for long-running module sessions.
