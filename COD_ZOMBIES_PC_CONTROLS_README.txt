Call of Duty: World at War: Zombies - keyboard and mouse controls
=================================================================

Gameplay automatically captures the mouse when a local player loads.
Mouse movement aims; left click fires. Returning focus restores gameplay
controls. The window title shows whether gameplay or the menu cursor is active.

  Esc                always brings the cursor out for the menus (pausing the
                     game in a level; pressed again it leaves the cursor out)
  W A S D, a push of either stick, Tab or middle mouse button
                     go back into play in a level, resuming a paused game
  Tab (or middle mouse button)   also bring the cursor out without pausing

Every control can be rebound for the keyboard, the mouse and a controller in
touchHLE_options.txt, which lists every binding, one per line.

CURSOR MODE (the default, for menus)
  The mouse works like a finger: click menu items, pause menu buttons and
  HUD icons normally.

MOUSE-LOOK MODE (for playing; the cursor is hidden and captured)
  Move mouse         look around / aim
  Left click         shoot (hold for automatic weapons)
  Right click        aim down the sights (click to toggle, or hold)
  Mouse wheel        switch weapon
  R                  reload
  Q                  switch weapon
  G                  throw grenade
  T                  switch grenade type
  V                  knife
  F                  interact: buy a weapon or perk, open a door, turn on the
                     power. Hold it to revive a player or rebuild a barricade.
                     This taps the prompt the game shows in the middle of the
                     screen, so it only does something when a prompt is up.

BOTH MODES
  W A S D            move (always at full speed; walking backwards is half
                     speed in the game itself)
  Esc                pause, with the cursor out to click the pause menu
  F12                switch between the window and fullscreen

Tips
  - No middle-click or Tab is needed after a level loads. Left click can
    recapture gameplay after manually releasing the cursor.
  - The right stick and R1 also recapture a loaded, unpaused game.
  - Alt-Tabbing away releases the mouse and held actions. Returning focus
    restores aiming, but never resumes a held shot. Pause menus keep the cursor.
  - Select either Dual Stick or Touch Screen in the game's Controls menu.
    The supported 1.5.0 game is detected automatically; no launcher change is
    needed when switching between those schemes. (Tilt aims by tilting the
    device, so the mouse doesn't aim there.)
  - In both schemes the mouse turns the view by the distance it moves, the
    same in either scheme: 0.15 degrees per mouse count at the default
    sensitivity. The view stops when the mouse stops; a flick faster than the
    game can turn is cut short rather than finished late. The right stick
    pushes the game's own stick, and stops the turn as soon as it is let go.
  - Left click/R1 presses the fire button with a separate finger. The aiming
    finger stays on its stick for as long as you play, so firing never moves
    or lifts it. Dual Stick's "Tap Aim To Fire" box is unticked automatically,
    because these controls shoot with the fire button, not with a tap on the
    aim stick.
  - In Touch Screen the game hands its aim area to the fire button while fire
    is held, so the aiming finger lands again right after each shot; you may
    notice a pause of about a tenth of a second in aiming after letting go.
  - Mouse sensitivity defaults to --mouse-look-sensitivity=6.0. Lower it in
    touchHLE_options.txt to slow aiming. In-game X/Y sensitivity also applies.
  - Increase --aim-stick-deadzone (for example 0.25) if the controller drifts.
    Values below 0.06 count as 0.06. While you are using the mouse, the right
    stick only aims when pushed past about a third, so a controller left
    connected can't take aiming away from the mouse.
  - A game controller also works, using the mapping built into touchHLE.

GAME CONTROLLER (in mouse-look mode)
  Left stick         move: a light push walks at half speed, and the speed
                     rises with the push to full speed near the edge
  Right stick        look around / aim
  R1 / Right shoulder  shoot
  L1 / Left shoulder   aim down the sights
  B / Circle         interact (hold to revive or rebuild, as with F)
  X                  reload
  Y                  switch weapon
  R2 / Right trigger   throw grenade
  D-Pad up           switch grenade type
  L2 / Left trigger    knife
  Options / Start    pause, and resume from the pause screen
  Share / Touchpad   switch between cursor and mouse-look mode
  (In the menus the d-pad moves the selection, Cross presses it and Circle
  goes back. A deliberate push of either stick goes back into play.)

Source: src/window/cod_controls.rs (controls) and src/window.rs (wiring).
Full patch against upstream touchHLE 9052ea39: cod-zombies-pc.patch.
The older COD_ZOMBIES_KBM_README.md, README_COD_CONTROLS.md, cod_zombies_controls.patch and
cod_zombies_environment.patch describe a previous version and are out of date.
