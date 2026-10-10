# World at War Zombies iOS PC

Play **Call of Duty: World at War Zombies iOS** on PC with **keyboard and mouse** or **gamepad** support.

## Installation

1. Download this repository (**Code > Download ZIP**) and extract it to a folder, for example `WAWZombies`.
2. Download **COD_Zombies_1.5.0.ipa** from:  
   https://archive.org/download/Call_of_Duty__Zombies_1.5.0_ios_3.0
3. Place `COD_Zombies_1.5.0.ipa` inside the `WAWZombies\game` folder.
4. Double-click **WAWZombies.exe**.

**WAWZombies.exe** starts the included Demonware server (`dw-server.exe`) when it needs one, logs you in, and launches the game.

The IPA is **not included with this release**. Each player must supply their own `COD_Zombies_1.5.0.ipa`.

If Windows says `VCRUNTIME140.dll` or `MSVCP140.dll` was not found, install the **Microsoft Visual C++ Redistributable (x64)**:  
https://aka.ms/vs/17/release/vc_redist.x64.exe

## Before Playing

Open `touchHLE_profile.txt` and change the player `name` to something recognizable.

That name identifies you when hosting and joining games, so every player should use a different name.

**Do not change the password after you have already played.** The game stores login information based on that password. If you need to change it, delete the `touchHLE_saves` folder first so the game can create fresh login data.

Players who share a server must all use the **same password** (the default `zombies` is fine). See [Names and passwords](#names-and-passwords).

## Controls

| Input | Action |
|---|---|
| **WASD** | Move |
| **Mouse** | Aim |
| **Left Mouse** | Fire |
| **Right Mouse** | Aim Down Sights |
| **R** | Reload |
| **Q / Mouse Wheel** | Switch Weapon |
| **G** | Grenade |
| **T** | Switch Grenade Type |
| **V** | Knife |
| **F** | Interact / Buy (hold to revive or rebuild) |
| **Esc** | Pause, and bring the cursor back for the menus |
| **Tab / Middle Mouse** | Toggle mouse-look / cursor |
| **F12** | Switch between window and fullscreen |

| Controller | Action |
|---|---|
| **Left Stick** | Move |
| **Right Stick** | Aim |
| **R1** | Fire |
| **L1** | Aim Down Sights |
| **R2** | Grenade |
| **L2 / R3** | Knife |
| **Circle / B** | Interact |
| **Square / X** | Reload |
| **Triangle / Y** | Switch Weapon |
| **D-Pad Up** | Switch Grenade Type |
| **Options / Start** | Pause and resume |
| **Share / Touchpad** | Toggle mouse-look / cursor |

Getting in and out of the game:

- **Escape always brings the cursor back** so you can use the menus. In a level it also pauses the game.
- In a level, pressing **W, A, S or D**, pushing **either stick**, or pressing **Tab / Middle Mouse** goes back into the game, resuming it if it is paused.
- Pressing **Resume** in the game's pause menu also goes back into the game.

In menus:

- **Arrow keys / D-Pad** move the selection.
- **Enter / Cross (A)** confirms the selection.
- **Circle (B)** goes back.

When touchHLE displays an on-screen prompt:

- Type normally to enter text.
- **Enter** accepts.
- **Escape** cancels.
- **Up / Down** cycles through known answers.

### Rebinding Controls

Every control can be rebound for the keyboard, the mouse and a controller in `touchHLE_options.txt`, which lists every binding, one per line:

```text
--cod-key-bind=reload:R
--cod-mouse-bind=fire:left
--cod-pad-bind=fire:r1
```

Each line gives an action and one or more inputs separated by commas, and replaces what that action had on that kind of input. Use `none` to unbind it. For example, to fire with R2 and throw grenades with R1:

```text
--cod-pad-bind=fire:r2
--cod-pad-bind=grenade:r1
```

- **Actions:** `forward back left right fire ads reload switch-weapon grenade grenade-type knife interact pause cursor`, and in the menus `menu-up menu-down menu-left menu-right menu-select menu-back`
- **Keys:** their names, such as `W`, `Space`, `LShift`, `LCtrl`, `F1`, `Keypad-Enter`
- **Mouse:** `left right middle mouse4 mouse5 wheel-up wheel-down`
- **Controller:** `cross circle square triangle l1 r1 l2 r2 l3 r3 options share touchpad dpad-up dpad-down dpad-left dpad-right`
- `--cod-pad-sticks=swap` moves with the right stick and aims with the left.

### Other Settings

All in `touchHLE_options.txt`:

| Option | What it does |
|---|---|
| `--fov=native` | Field of view. `native` is the game's own (about 58 degrees across); a number from 50 to 120 sets the degrees across, e.g. `--fov=75` |
| `--scale-hack=1` | Render resolution. `2` or `3` is sharper but heavier |
| `--mouse-look-sensitivity=6.0` | Mouse aiming speed |
| `--gamepad-look-sensitivity=1.0` | Right stick aiming speed (0.1 to 4.0) |
| `--aim-stick-deadzone=0.10` | Raise it if your right stick drifts |

Restart the game after changing settings.

## Hosting and Joining

Co-Op games are played through a **server**: every player connects to the same `dw-server.exe`, which logs everyone in and passes the game between them. One player **hosts** the match in their game and the others **join** it. Nobody but the server needs to open ports.

Choose where the server runs:

- **On the host's PC** (simplest). WAWZombies.exe starts it automatically.
- **On another PC or a VPS**, running `dw-server.exe` on its own, without the game.

### Host on Your PC

**Host (server on this PC):**

1. Leave `touchHLE_options.txt` as it is (`--dw-mode=host`).
2. Start **WAWZombies.exe**. It starts `dw-server.exe` for you.
3. Allow `dw-server.exe` through Windows Firewall if Windows asks.
4. Give the other players your address:
   - Same network: your local IP address (run `ipconfig` and look for **IPv4 Address**, e.g. `192.168.1.20`).
   - Different networks: your public IP address or a DDNS host name, after forwarding the ports below to your PC.
   - Virtual LAN (ZeroTier, Tailscale, Radmin VPN): your address on the virtual network. No port forwarding is needed.
5. Open **Co-Op > Wi-Fi** and create a game. Keep the lobby open while the others join.

**Joiner:**

1. In `touchHLE_options.txt`, change these two lines, using the host's address:

   ```text
   --dw-mode=join
   --dw-server=192.168.1.20
   ```

2. Start **WAWZombies.exe**. It does not start a server of its own in join mode.
3. Open **Co-Op > Wi-Fi**, choose to join a game, and pick the host's game.

Ports to forward to the server PC when players are on different networks:

| Port | Protocol | Purpose |
|---|---|---|
| **3074, 3075, 3076** | TCP | Login and online services |
| **3077** | TCP | Game relay |
| **3074, 3478** | UDP | STUN |

Joiners never need to forward ports.

### Run a Server Without the Game

Double-click **dw-server.exe**. It runs on its own in a console window and keeps the lobby open even with nobody playing. Close the window to stop it. A game in host mode on the same PC uses the running server instead of starting another.

For a dedicated server PC or VPS:

1. Copy `dw-server.exe`, `config.json` and `players.txt` to it.
2. In `config.json`, set `"hostname"` to the server's public address.
3. Open the ports in the table above (TCP 3074-3077, UDP 3074 and 3478).
4. Start `dw-server.exe`.
5. **Every** player, including whoever hosts the match, uses join mode with the server's address:

   ```text
   --dw-mode=join
   --dw-server=your.server.address
   ```

`dw-server.exe` is a Windows program. A Linux VPS needs the server built from source.

### Rooms

Everyone on the same server with the same `--relay-room` sees the same games. Give a group its own room name (letters, numbers, `_` and `-`) to keep it separate from other players on a shared server:

```text
--relay-room=my_friends
```

A room name is not a password.

### Names and Passwords

The server works out each player's login from their password, so it has to know it. `players.txt`, beside `dw-server.exe`, lists the players, one per line:

```text
# name     password   address (the IP the player connects from)
Host       zombies
Friend     zombies    192.168.1.42
```

- When WAWZombies.exe starts the server, it writes the host's own line from `touchHLE_profile.txt`.
- A line without an address lets anyone with that password in. Extra players get a number after the name, such as `Host1`.
- Add a line with a player's address to give them their own name.
- To keep your own edits, delete the first line that `WAWZombies.exe` writes into `players.txt`.

If a player cannot log in, check that their password matches the server's `players.txt`.

### Playing Without a Server (Same Network Only)

Replace `--net-relay` with `--no-net-relay` in `touchHLE_options.txt` on every PC. Games are then found directly on the local network, and **F2** lets you type in the address of a PC to look for games on.

## Important Files

| File | Purpose |
|---|---|
| `touchHLE_profile.txt` | Player name and password |
| `touchHLE_options.txt` | Settings, server mode and control bindings |
| `config.json` | Server settings (address, ports) |
| `players.txt` | Players the server knows (written by WAWZombies.exe) |
| `touchHLE_netplay.txt` | Saved addresses used by F2 |
| `touchHLE_log.txt` | Main game and emulator log |
| `dw-server-log.txt` | Server log, when WAWZombies.exe starts the server |
| `touchHLE_launcher.txt` | Launcher and server startup log |

Save backups are stored in:

```text
touchHLE_saves/<slot>/history
```

Run:

```text
WAWZombies.exe --help
```

for all the available options.

## Credits

Built on [touchHLE](https://touchhle.org/) and [Open BitDemon](https://github.com/Laupetin/open-bitdemon-emulator).
