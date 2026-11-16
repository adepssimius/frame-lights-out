# Status Light for Steam Frame

A [Framey](https://github.com/chaosfox26/framey) plugin that turns off the
status LED on the side of the Steam Frame. It adds a **Status light** toggle to
SteamVR's Quick Settings, under Airplane mode, and a tab in Framey's panel.

Handy when you use the headset in a dark room and the light bothers someone
else.

Unofficial, not affiliated with Valve. Tested on one headset in November 2026;
a Steam update can break it.

## Install

You need Framey running on the headset.

- **Framey Settings tab:** paste this link and press Install:
  `https://github.com/adepssimius/frame-led/releases/latest/download/frame-led.zip`
- **Framey App:** install `frame-led.zip` from the
  [latest release](https://github.com/adepssimius/frame-led/releases/latest),
  or give it this repository's link.
- **By hand:** copy this folder to `~/framey/plugins/frame-led` and press
  "Reload modules" in Framey's Settings tab.

## How it works

- No root. The LED is `/sys/class/leds/rgb:status`, writable by the `leds`
  group, and the `steamos` user is a member.
- While the light is switched off, the backend watches the LED and darkens it
  again whenever Valve's `ledcontrol` daemon repaints it (charger plugged in,
  low battery, wake).
- The setting is saved in `~/.config/frame-led/state.json` and applied again
  when Framey starts.
- Switching the light back on, or disabling or removing the plugin, hands the
  LED back to `ledcontrol`. To make the daemon repaint, the plugin briefly
  rewrites `/run/deckardcharger/vr_state` and restores it.

## Limits

- While the headset is asleep nothing can run, so the LED shows whatever
  `ledcontrol` set just before sleep, for example the charging colour.
- The Quick Settings row is a copy of Valve's Airplane mode row. It works with
  the laser pointer and hands; controller D-pad focus skips it.
- If a Steam update restructures Quick Settings the row can disappear. The
  Framey tab keeps working.

## License

MIT
