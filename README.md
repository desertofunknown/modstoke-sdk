# Modstoke SDK

This repository is for people writing mods against Modstoke Loader. The SDK is still part of the loader's `OpenACAI.Endnight.Loader.Core.dll`; there is no separate SDK DLL or NuGet package to install. The example here builds against a Core DLL from the same loader build you plan to use in game.

The current loader branch targets .NET 11 RC2. Its public release and in-game acceptance are still being worked through, so treat this as a development example, not a tested mod download.

## Build the example

Install the .NET SDK selected by [global.json](global.json). Then point `OpenACAICorePath` at `OpenACAI.Endnight.Loader.Core.dll` from a matching loader build or an installed loader:

```powershell
dotnet build examples/WorldConditions/WorldConditions.csproj --configuration Release "-p:OpenACAICorePath=C:\Games\Sons Of The Forest\OpenACAI\Runtime\OpenACAI.Endnight.Loader.Core.dll"
```

Change the path to your own game install. The Core DLL is a build dependency; the example does not copy it into its output. The build produces `OpenACAI.Examples.WorldConditions.dll` and `openacai.mod.json` under `examples/WorldConditions/bin/Release/net11.0/`.

To try it in a local game with a matching loader, stop the game and copy those two files into:

```text
<Sons Of The Forest>/OpenACAI/Mods/WorldConditions/
  openacai.mod.json
  OpenACAI.Examples.WorldConditions.dll
```

Restart the game. The example is designed to show a **World Conditions** page and settings in Extensions. Its Refresh action reads local clock and weather snapshots; it does not change either one. The source currently compiles against the SDK, but its loading, layout, interaction, and scene transitions have not yet been verified in game. See [the example guide](examples/WorldConditions/README.md) before adapting it.

## What to reference

The current APIs use `OpenACAI.Loader` and `OpenACAI.Sons` namespaces in Loader Core. Legacy `SonsSdk.dll` is packaged by the loader for compatibility with older RedLoader mods; it is not the Modstoke SDK assembly. `WorldConditions.csproj` references only Loader Core. A mod that changes multiplayer or server state must check authority on the host or server; a menu button on a client is not permission.

The matching [Modstoke Loader repository](https://github.com/desertofunknown/modstoke-loader) is being prepared for a curated source import. Until that import is complete, use Loader Core from a matching local build or installation; this SDK repository alone cannot build Loader Core. The example's manifest and assembly must travel together. Give your own mod a distinct ID, assembly name, entry type, and menu/provider IDs.

## License

The example source is GPL-3.0-or-later; see [LICENSE](LICENSE) and the SPDX headers in the C# files. Game files and Loader Core are not included here.

