# SusAC+ 2.0

SusAC+ is an updated version of the existing SusAC Paper plugin. It keeps the original `/sus` staff workflow, flag storage, GUI, chat checks, permissions, and configuration structure while adding behavioural detections aimed at the kinds of movement/combat/automation modules present in the supplied Anubis client JAR.

## New behavioural detections

- **Jesus** — repeated horizontal movement while standing on liquid without swimming.
- **NoFall** — tracks a descent and flags repeated landings after a substantial drop when no fall-damage event was observed.
- **ElytraFly** — checks unusually high horizontal movement per server tick while gliding.
- **Scaffold** — buffers repeated underfoot/near-foot block placements while the player's view pitch is unusually shallow.
- **KillAura** — flags repeated attacks against targets well outside the server-observed view cone.
- **AutoTotem** — flags repeated, unusually rapid offhand inventory actions.

The existing checks also cover parts of the client’s AutoClicker, Speed, Fly, multi-target combat, mining/ore-finding, and fast-placement behaviour (including WallTrack-style suspicious tracking patterns). These are behavioural overlaps, not proof that a particular module is enabled.

Existing detections remain in place, including Speed, Fly, Reach, WallHit, MultiAura, AutoClicker, MacroClick, XRay, Nuker, BreakReach, FastPlace, FastEat, OmniSprint, AutoWalk, WallTrack, and the chat checks.

## Important server-side limits

A normal Paper plugin does not receive trustworthy client-mod/module state. It cannot directly confirm client-only rendering features such as ESP, Fullbright, X-ray overlays, freecam camera rendering, or visual HUD modules. Some client features (Triggerbot reaction timing, timer/packet pacing, inventory movement while moving, no-slow, boat noclip, Freecam, and certain macros) also need packet-level or server-specific evidence that this Bukkit-event implementation does not have. BoatFly is partly covered by the generic movement checks, but a dedicated boat-physics check is not included. SusAC+ therefore detects observable behaviour, not the mere presence of Anubis.

Several detections are heuristic. Tune their thresholds for your server's latency, movement plugins, custom items, and game modes. Do not auto-ban from a single flag; review repeated flags and their context. The existing `sus.bypass` permission and creative/spectator exemptions are retained.

## Build

Requires Java 21 and Maven. From this folder run:

```sh
mvn package
```

The plugin targets Paper API `1.21.4-R0.1-SNAPSHOT`, matching the original project. The source archive is supplied because Maven is not installed in the build environment used to prepare this update; the Java project has not been compiled here.
