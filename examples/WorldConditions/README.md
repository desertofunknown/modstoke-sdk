# World Conditions example

This example shows the smallest useful Modstoke-native menu: a read-only action that captures the local clock and weather, plus a setting that changes how the captured time is displayed. It uses Loader Core without direct BepInEx, RedLoader, SonsSdk, or game interop references.

Build and install it using the commands in the [repository README](../../README.md). The `openacai.mod.json` file names `Mod.Initialize` as the entry point and `Mod.Shutdown` as its shutdown callback. Both the manifest and DLL must be in the same `OpenACAI/Mods/WorldConditions` directory. Do not put a second Loader Core DLL in that directory.

`Mod.cs` registers and unregisters the menu and settings providers. `WorldConditionsProvider.cs` reads game state through the SDK on the initialized game thread, then keeps managed snapshots for menu rendering. Each observation has a timestamp. A failed read reports its own status instead of presenting a fake zero clock or clear weather.

The example can run on a host or client without requiring other players to install it. It adds no remote administration endpoint. If you adapt it to change shared world state, enforce permissions and authority on the host or server. UI confirmation flags are not an authorization system.

The example compiles against the current API. In-game loading and UI behavior still need verification.

