# startgame

CLI/Steam custom game launching helper

## Usage:

```sh
startgame ${options} -- %command%
```

## Options:

- `--amdpro`
  Forces VK ICD to amdpro (for AMD GPU's only)

- `--radeon`
  Forces VK ICD to radeon (for AMD GPU's only)

- `--dxr`
  Enable DXR in VKD3D

- `--fsr=[0-5]`
  Foces AMD's FidelityFX

- `--gamescope`
  Enable Gamescope

- `--llvm`
  Disables ACO (for AMD GPU's only)

- `--log`
  Enable Proton, Wine and DXVK's logs

- `--log-mfplat`
  Enable Wine's mfplat logs

- `--nomango`
  Disables MangoHud

- `--nsdl{,=32,=64}`
  Force system's SDL libraries

- `--nodcc`
  RADV's nodcc (for AMD GPU's only)

- `--nox`
  Remove X11 and XWayland access (forces Wayland-only)

- `--singlecore`
  Simulate singlecore CPU topology

- `--soldier`
  Enable Steam Soldier (see #notes)

- `--nocapture`
  Don't force VkCapture

- `--wayland`
  Don't force XWayland

- `--zink`
  Force Mesa's OpenGL/Gallium to Vulkan

- `--term`
  Opens a terminal instead of the game (exposes game command in `"$GAME_CMD"`)

## Requirements:

- ArchLinux

- `gamemode`, `lib32-gamemode`

- `mangohud`, `lib32-mangohud`

- `obs-vkcapture`

- `gamescope` (optional)

- `sdl2`, `lib32-sdl2` (optional)

- Wine with FSR pattches (optional)

## This script by default:

- Enables mangohud;

- Disables logs from Proton, Wine and DXVK;

- On Wayland, forces games to use XWayland (with `SDL_VIDEODRIVER` and `XDG_SESSION_TYPE`);

- If available, enables VkCapture;

- Skips Steam Soldier (needs manual action, see #notes);

- Logs stdout and stderr to `"/tmp/game-user-timestamp.log"`.

## Notes:

- Set `$TERM` for `--term`;

- Gamescope parameters can be configured in `"~/.config/gamescope-flags.conf"`;

- For enabling/skipping Steam Solider with `--soldier`, you'll need this line prepended (after shebang) in `"~/.steam/steam/steamapps/common/SteamLinuxRuntime_soldier/_v2-entry-point"`:

```sh
if [[ -z "${STEAM_ENABLE_SOLDIER:-}" ]]; then shift 4; exec "${@}"; fi
```

## Examples:

- Portal 2, native in Wayland: `startgame -w --nsdl %command% -novid -vulkan`

- Left 4 Dead 2, native in Wayland: `startgame -w --nsdl=32 %command% -novid -vulkan`