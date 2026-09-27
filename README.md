# th06nc-mouse-control
Mouse controls for Touhou 6 New Classic, with direct movement and an optional normal-speed limit
TH06 New Classic Mouse Control 1.2

Controls
Move the mouse: move the character immediately, without catch-up motion.
Left click: fire.
Right click: focus and half mouse sensitivity for precise dodges.
First side button (Back): bomb. Choose the other side button under F11 > Mouse.
F10: toggle mouse control.
F11 > Mouse > Direct movement: switch between direct movement and the original normal-speed cursor-following mode.
Save to touhou_hfr.ini: keep your settings.

In direct mode, the cyan crosshair marks the character's actual position. Mouse displacement is applied at the presentation rate; the character sprite bypasses delayed interpolation. Other sprites retain your smoothing setting. The pointer is repositioned onto the character during active play, keeping it aligned even when using reduced sensitivity or reaching a playfield boundary.

Right-click changes sensitivity immediately, without a catch-up animation or jump when released. Menu, pause, lost focus and keyboard-control transitions reset the mouse anchor so returning to play does not jump the character. Use the keyboard in menus. Keyboard/controller directions take priority while held. F10 releases mouse control.

Direct movement writes the live player position. With the optional speed limit off, it removes the normal character speed limit. Collision and other native gameplay remain at 60 Hz unless you separately enable HFR's projectile sub-stepping. Native replay files do not record these direct positions, so they cannot reproduce direct-mode play faithfully. Disable mouse control before replay playback.

Optional speed limit
Under F11 > Mouse, enable Direct movement, then check Limit to normal character speed. Use Save to touhou_hfr.ini to keep the selection. This option is initially off, preserving the existing unrestricted mode.
The limit uses the current character's normal speed, or focused speed when holding right-click, scaled by elapsed time and game speed. Diagonal swipes share the same total speed limit. Small movements remain immediate. Fast swipes discard excess travel instead of queuing it, and the pointer is kept on the character. Right-click retains its half sensitivity. Long stalls are capped to one native frame of travel.
The speed cap does not make direct-mode replays compatible. The original cursor-following mode remains available by turning Direct movement off.
Additional automated checks cover two character speeds, focused/unfocused movement at 60, 144, 360 and 1000 Hz, diagonal direction and speed, slow precise movement, no residual motion, stalls, duplicate polls, game-speed changes and menu toggling.

Installation
Close the game. Place dxgi.dll, touhou_hfr64.dll and touhou_hfr.ini beside th06nc.exe, then launch through the Steam interface.
For an existing HFR installation, back up its DLL and INI, replace touhou_hfr64.dll, and merge these settings into the existing INI instead of overwriting your preferences:
[mouse]
enabled=1
direct=1
speed_limit=0
bomb_button=1

The existing HFR loader can be retained. To revert, close the game and restore the backed-up DLL and INI. The original game executable is not modified.
Supported executable SHA256:
48630a42a2eb6762d0db2a7e0d151203efbe67220fef7d2f9d0d51857928ac82
Verification

Automated tests exercise the actual controller with simulated device input: direct displacement, display-rate sampling, half-sensitivity focus, no release jump, boundary reversal, menu/pause/focus/keyboard transitions, button edges, viewport scaling, and player-only smoothing bypass. The retained follow mode passes 320 movement destinations. Input detouring is tested on an inert copy of this game's code. The original x64 regression suite and all 31 executable signatures pass.

Version 1.2 physical gameplay testing is pending. Test results accompany this package.
Source and build
The source archive includes README-MOUSE.md and tools/test_mouse.c.
Run build64.ps1 -Compiler <path-to-64-bit-MinGW-gcc.exe>.
Built with GCC 16.2.0 from w64devkit 2.10.0.
Run test64.ps1 against the supported executable for the original regression suite.
Compile tools/test_mouse.c with build/obj64/{buffer,hook,trampoline,hde64}.o and -lbcrypt, then run it with the game executable path.
Based on Touhou HFR 0.13-test: https://github.com/vittorioromeo/th12_hfr
Dear ImGui and MinHook license notices are included.
