QUICK STACK AREA 1.1.0  (EML data mod + Ultimate ASI Loader plugin)
====================================================================

What it does
  Changes the size of the area of the Quick Stack Station and the Large Quick
  Stack Station: the square they draw, inside which your enchanted chests
  receive items when you press E on the station.

  - X and Y (the two floor directions) and the height can each be set
    separately, so the area can be a long rectangle as well as a bigger or
    smaller square.
  - The area can also reach DOWN below the station (new in 1.1.0), so a
    station on the ground floor can fill chests in the basement.
  - The outlines change with it: the outline you see while placing a station,
    and the flash when you press E.
  - Turn a station with R and the area turns with it. The outlines follow too
    (this part needs the plugin, see below).

  Nothing else about quick stacking changes: chests still need "Receive Quick
  Stacking" switched on and must be in the same base as the station, and one
  quick stack still fills at most 32 chests (a game limit).

The two parts
  mods\quick-stack-area\     the data mod (Enshrouded Mod Loader, EML). Sets the
                             area and the outlines. Needed by whoever runs the
                             world AND by each player.
  Scripts\QuickStackArea.asi the plugin (Ultimate ASI Loader). Only turns the
                             outlines with a station that is not square. Players
                             only; not needed if X = Y for both stations.

Requirements
  - Enshrouded Mod Loader (EML): dbghelp.dll from
      https://github.com/brabb3l/kfc-parser/releases
    next to enshrouded.exe (or the server's .exe).
  - For the plugin: Ultimate ASI Loader by ThirteenAG (x64):
      https://github.com/ThirteenAG/Ultimate-ASI-Loader/releases
    Its dll (dinput8.dll or winmm.dll) goes next to enshrouded.exe. You may
    already have it: look for a "Scripts" folder with other .asi files.

Which download do I need?
  quick-stack-area-1.1.0.zip         PLAYERS: solo, hosting a co-op world, or
                                     joining a server. Data mod + plugin.
  quick-stack-area-server-1.1.0.zip  DEDICATED SERVERS: the data mod only.

Who decides - and which config.txt counts
  - Which chests receive items is decided by whoever runs the world: your own
    game in solo or when you host, or the dedicated server. So on a dedicated
    server, the SERVER's config.txt sets the real area.
  - The outlines (while placing, and the flash on E) are drawn by each player's
    own game, from that player's config.txt.
  If the two differ, the outline shows one size and the chests use another.
  Use the SAME config.txt on the server and on every player's game.
  A player without the mod on a modded server still gets the server's area,
  but sees the game's normal outline. A modded player on a server without the
  mod sees the bigger outline, but the chests use the game's normal area.

INSTALL - PLAYERS (solo, hosting, or joining a server)
  1. Close the game.
  2. Extract quick-stack-area-1.1.0.zip into the game folder (the one with
     enshrouded.exe), so you have:
       ...\Enshrouded\mods\quick-stack-area\mod.json
       ...\Enshrouded\Scripts\QuickStackArea.asi
  3. Set your sizes in mods\quick-stack-area\config.txt (see below). When you
     join a server, use the server's config.txt instead.
  4. Start the game. Friends who join your hosted world install it too, with
     your config.txt.

INSTALL - DEDICATED SERVER
  1. Stop the server.
  2. Extract quick-stack-area-server-1.1.0.zip into the server folder (the one
     with enshrouded_server.exe), so you have:
       <server root>\mods\quick-stack-area\mod.json
  3. Set the sizes in its config.txt and start the server.
  4. Give your players the same config.txt for their own install.

SETTINGS (mods\quick-stack-area\config.txt)
  quickStackSizeX / quickStackSizeY / quickStackHeight
      the normal station (mod default 20 / 20 / 4; game 16 / 16 / 4)
  largeQuickStackSizeX / largeQuickStackSizeY / largeQuickStackHeight
      the large station (mod default 28 / 28 / 8; game 24 / 24 / 8)
  quickStackDepthBelow / largeQuickStackDepthBelow
      how far the area reaches below the station (default 0 = the game's
      normal, just below the floor the station stands on). 0 to 512.
      Height is how far it reaches up; the outline grows down with it.
  Full side lengths, 1 to 512. X and Y are the station's directions before you
  turn it; turned 90 degrees, they swap.
  enabled      true/false
  logDetails   true = more detail in the logs (troubleshooting)
  Restart the game (and the server) after a change.

  Example: a long strip along a wall of chests
    quickStackSizeX = 40
    quickStackSizeY = 12

  Example: chests in the basement below the station
    quickStackDepthBelow = 8

CHECK IT WORKED
  Open the newest file in the "logs" folder next to the game (or server) .exe and
  look for a line like:
    [Quick Stack Area] v1.1.0 on client: Quick Stack Station 40x12 h4 below0 (was 16.0x16.0 h4.0)
        area=ok outline=ok | ... | preview outlines patched: 6 (...)
  ("on server" on a dedicated server.) FAILED, "found 0 of 2 station templates"
  or "preview outlines patched: 0" mean a game update changed the data and the
  mod needs updating.
  The plugin writes quick-stack-area.log next to enshrouded.exe; it should say
  "outline fix ready". After a game update it may say "not found": the area
  still works then, only a turned non-square outline points the wrong way.

UNINSTALLING
  Delete mods\quick-stack-area and Scripts\QuickStackArea.asi. Placed stations
  go back to the game's sizes.

Credits
  The settings reader and safe field helpers of the data mod follow Auto Loot
  Plus by Dellemann (MIT License, see licences\MIT LICENSE.txt).
  Requires the Enshrouded Mod Loader by brabb3l and the Ultimate ASI Loader by
  ThirteenAG.
