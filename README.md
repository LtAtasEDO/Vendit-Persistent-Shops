# Vendit Persistent Shops for use with Cyberpunk RED — Foundry VTT v12
Persistent, scene-aware vending machines for Cyberpunk RED with 2077/2045 era skins, generated Monk's Tile Binder, active-scene CitiNet location pings, configurable player proximity, dynamic stock, Simple Calendar background traffic, curated pricing and safer Tile template lifecycle handling.

Module creation assisted by AI from macro v3.0.3, legacy macro can be found in Cyberpunk Red Foundry VTT Discord content sharing.

The bundled Binder icon is now a CC0-based SVG asset recolored for Vendit using `#E64539` on `#1B1F21`, replacing the earlier WebP-based icon.

Version **1.3.0** keeps the existing `vendit.db` world setting while polishing the module into a dedicated Vendit retail interface for both 2077 and 2045.

## Installation

1. Back up the world.
2. Replace `{Foundry User Data}/Data/modules/vendit` with the `vendit` folder from this ZIP.
3. Restart Foundry VTT and enable **Vendit™ Persistent Shops**.
4. Hard-refresh connected browsers.
5. OR use Foundry Module installer via: [Manifest URL](https://github.com/LtAtasEDO/Vendit-Persistent-Shops/releases/latest/download/module.json)

Existing shops, dynamic settings, stock, prices, sale schedules, and Tile flags remain under the same module ID/database.

## Clickable item descriptions

Click a product's **name or image** in the player shop or GM Preview to open a read-only item preview. It shows the description, available item details, market value, and current Vendit price. Sold-out products can still be inspected.

Inspection does not purchase an item or open its editable sheet. With an active GM, the preview works for stock from compendiums players cannot normally open. Only the offered item's public description/details are sent; secret blocks and interactive document links are removed. Without an active GM, the source Item must be readable by the player. Missing sources show a warning.

## Compatibility

Foundry VTT **12** (verified **12.343**); Cyberpunk RED **0.92.1+** (verified **0.92.4**).

| Recommended module | Minimum | Verified | Maximum |
| --- | --- | --- | --- |
| Simple Calendar | 2.4.17 | 2.4.18 | 2.4.18 |
| Monk's Active Tile Triggers | 12.01 | 12.02 | 12.02 |

These integrations remain optional. Clickable item inspection has been live-validated by the GM/player.

## Vendit UI skins

- **2077:** deep-black retail terminal with cyan chrome and yellow machine accents.
- **2045:** the same Vendit layout with the established `#E64539` redline accent and warm amber secondary highlights.
- CitiNet card styling/content is preserved, but the action button now **PINGs the Vendit location** instead of opening the shop remotely.

## Generated Monk's Active Tiles binder

The Binder now uses the bundled `modules/vendit/assets/Vendit.svg` icon. Existing module-generated Binder macros are automatically updated to the bundled Vendit icon on startup, while an unrelated/custom macro that merely shares the name is left alone unless you explicitly use **Create / Repair Binder Macro**.

The module automatically creates **Vendit™ Binder** for the primary GM if it is missing. It can also be repaired from Vendit Options or Dynamic Network.

Use the generated macro as the Run Macro action on Vendit Tiles. For Tile-bound Vendits, leave the MATT argument field blank. Static/private machines may continue using `id=YOUR-ID`.

Canonical Binder command:

```js
return game.vendit.run({
  args: typeof args === "undefined" ? null : args,
  tile: typeof tile === "undefined" ? null : tile,
  token: typeof token === "undefined" ? null : token,
  actor: typeof actor === "undefined" ? null : actor
});
```

## Player proximity & CitiNet location pings

Tile-bound Vendits are physical machines. Players must be within **2 grid spaces** by default before the player shop opens. The range can be changed under **Vendit™ Options → Player Interaction Range (grid spaces)**. GMs can Preview from anywhere.

The generated Binder forwards both the triggering Tile and Token, so existing MATT Vendit Tiles do not need a separate Distance action. Manually bound or auto-generated Tiles inherit the proximity gate automatically.

CitiNet flash-price cards no longer provide remote shopping. Their button is **PING LOCATION**: it pans to the bound Vendit Tile and triggers Foundry's native map ping on the active Scene. Only Vendits with a physical Tile binding are eligible for automatic CitiNet location ads. Old chat cards with the former OPEN button are also treated as pings after upgrade.

## Auto-Tile Template

The Auto-Tile Template is a **blueprint**, not a master inventory. It copies the selected Vendit's dynamic configuration, source tables/packs, curated pools, quantity/cycle settings, and sale rules to newly created Tiles whose name/image matches the configured keywords.

Each matched Tile receives:

- a unique Vendit ID;
- its own Scene/Tile binding;
- freshly generated dynamic inventory.

The template machine's current live inventory is **not** copied.

You can remove the template in either location:

- **Dynamic Vendit → Clear Auto-Tile Template**, or
- **Dynamic Network → Clear Template**.

Automatic Tile creation can remain enabled with no template; in that state new matching Tiles use the global Vendit defaults.

## Dynamic network behavior

- 3–6 generated products by default.
- 2–3 Simple Calendar day inventory cycles by default.
- Background NPC purchases and occasional restocks.
- Weighted 75–115% pricing with 100% most common and discounts rare.
- CitiNet sale pings only from Vendits on Foundry's globally active Scene.
- Daily CitiNet ping range: **0–48**, configured in **Dynamic Network**; the default remains **1–3**. Set both Min and Max to 48 for 48 scheduled opportunities per standard in-world day.
- Pings are spread across the advertising window (09:00–22:45 in a standard 24-hour calendar). A scene still needs an eligible sale-enabled Vendit; these are network-wide opportunities, not guaranteed messages per scene.
- Changing the ping range rebuilds the current day schedule on the next calendar tick.
- Skipped alarm times collapse into one message rather than spamming chat.

## Data and binding safety in 1.2.x

- Rebinding a Vendit clears its previous direct Tile flag.
- Binding a Tile already owned by another Vendit repairs the old reverse link.
- Deleting a Vendit clears its direct Tile flag and removes it as the Auto-Tile Template.
- Changing a bound Vendit's ID updates its Tile flag and template reference.
- Auto-Tile clones no longer inherit the template machine's live/static inventory.
- Player purchases are GM-authoritative and serialized, preventing double-clicks or two clients from both claiming the final unit. Only Foundry's active GM processes a purchase when multiple GMs are connected.
- If Item delivery or stock persistence fails, the purchase rolls back the created Item where possible and refunds the buyer.
- Duplicate Vendit IDs are rejected before they can overwrite another machine.
- A chat-render failure cannot turn an already-completed dispense into a false purchase failure.

## API

```js
game.vendit.openManager();
game.vendit.openOptions();
game.vendit.openShop("YOUR-VENDIT-ID");
game.vendit.openDynamicManager();
game.vendit.ensureBinderMacro({ repair: true, notify: true });
```

Legacy `game.venditrun(...)` remains available.

## Legal / Homebrew Content Policy

This is unofficial homebrew content for use with Cyberpunk RED.

This project is provided free of charge under the R. Talsorian Games Homebrew Content Policy.

Vendit Persistent Shops for use with Cyberpunk RED is unofficial content provided under the Homebrew Content Policy of R. Talsorian Games and is not approved or endorsed by RTG. This content references materials that are the property of R. Talsorian Games and its licensees.

Cyberpunk RED and related properties are the property of R. Talsorian Games and their respective licensees.

## Credts and Assets Notice

This project is unofficial fan tooling and is not affiliated with R. Talsorian Games, Foundry Gaming LLC, or CD PROJEKT RED.

As of v1.2.6 the bundled `assets/Vendit.svg` asset used from SVG Repo **Vending Machine**, **CC0 License** is recolored with Core System styling and may be recolored or further refined as needed for future releases. Full attribution and the license text are included in THIRD_PARTY_NOTICES.md.
