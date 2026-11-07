# Changelog

All notable changes to FirstTilt are listed here. This file is the public release notes: each
version's section is published with its release on
[FirstTilt-Releases](https://github.com/WoolawayWx/FirstTilt-Releases/releases) and shown in the
app's "What's new" window, so write entries for people using the app, not for the code.

Add notes under **Unreleased** as you work. `cargo xtask release <patch|minor|major>` moves them
under the new version when you release.

## [Unreleased]

## [0.6.1] - 2026-11-07

### Fixed
- On Windows, FirstTilt now asks Explorer to refresh its icons the first time you start a new version, so shortcuts and the taskbar stop showing an old icon left over from a previous version.

## [0.6.0] - 2026-11-07

### Added
- FirstTilt has a browser viewer with site and product selection, live scans, and playback. Choose the WoolawayWx radar feed or process NEXRAD Level II scans on your device.
- Settings now gives you access to local diagnostics. FirstTilt keeps recent desktop session logs and Rust panic reports, and the web viewer can download a report of recent errors.
- FirstTilt can send limited crash reports automatically to WoolawayWx. Automatic reporting is on by default in builds with a report collector. You can turn it off in Settings or review and send a report yourself.

### Fixed
- Dragging the "maximum frames" slider no longer deletes loaded frames along the way, and dragging the polling-interval slider no longer restarts live updates on every step. Both apply when you let go.
- The P shortcut now saves the product you land on and skips products that have no data. Single-letter shortcuts no longer fire when Ctrl, Cmd, or Alt is held.
- Esc now closes the update prompt.
- Map layer order set in Settings is now remembered between launches, and the move buttons are disabled at the ends of the list.
- Live radar updates are now merged by compass angle instead of by each volume's radial order, which could blank part of a sweep or draw part of it twice when a new volume started at a different angle.
- Radar downloads and listings now time out and retry instead of hanging forever, and a network problem is reported as one rather than as "no scans available". Switching sites no longer waits on the old site's live catch-up.
- Switching product or tilt while a live update arrives no longer mixes products on the timeline or leaves frames blank.
- The live watcher no longer re-processes the same partial volume while waiting for new data.
- Disabled playback buttons now explain why. Color-table import messages clear on their own.
- Choosing a screenshot, animation, color table, or archive no longer freezes FirstTilt while the file dialog is open, and live updates no longer stall the interface while they are merged.
- Zooming in is limited to a level where radar and map lines stay steady instead of jittering.
- The web viewer is more dependable on slow connections: downloads show progress, retry automatically if the connection drops, and have a Retry button if they fail.

### Changed
- Settings is now organized into pages (General, Radar, Map, Alerts, Labels, About & diagnostics) with reset buttons for the basemap, alerts, and labels, an interface size control, and a diagnostics folder button.
- New shortcuts: R shows or hides radar data, T cycles the elevation tilt, H loads history, A opens the Alerts panel, 1/2/4 choose the number of map panes, and Ctrl/Cmd+, opens Settings. A new top-bar button toggles radar data too.
- The timeline lets you drag to scrub through frames and shows each frame's time when you hover it. Icon buttons now have names for screen readers.
- The web viewer works better on phones (pinch and double-tap zoom, Previous/Next stay on screen), lets you type to search for a site or tap one on the map, shows the elevation angle, and can be panned from the keyboard. Background tabs stop polling.
- Live radar playback and the IEM feed use less memory and bandwidth, and the radar cache is written safely.
- FirstTilt has a new look for its icon and logo, in the WoolawayWx burgundy, ink and cream: an FT monogram under a radar scope with a lightning-bolt sweep. It replaces the rainbow icon in the app, the installers, the macOS disk image, and the browser viewer's tab icon and header.
- The desktop app and browser viewer use the same colors as the new logo: warm ink backgrounds, cream text and highlights, and burgundy for selected items and primary buttons. Radar and alert colors are unchanged.

## [0.5.1] - 2026-09-27

### Fixed
- Fixed in-app updates on macOS failing with "failed to unpack `._FirstTilt.app`" — the signed
  update archive could include a stray macOS metadata file alongside the real app.
- An available update now shows a centered popup the first time this session, instead of only a
  small toolbar icon that was easy to miss. The full details still live in Settings too.

## [0.5.0] - 2026-09-27

### Added
- Press Cmd (macOS) or Ctrl (Windows/Linux) + Plus/Minus to scale the size of the whole interface,
  and +0 to reset it. This scales the UI itself, not the window.
- Archive viewer: open a folder or a selection of local NEXRAD Level II archive volume files
  to view them as a fixed loop, separate from the live site — a new header button, or
  Settings → Archive. "Back to Live" returns to whatever site was showing. Weather alerts and
  the live-status/History controls are hidden while an archive is open, since they don't apply
  to historical data.
- Differential Phase is now a selectable product, alongside the existing five.
- Each pane can now show a different elevation tilt instead of always the lowest one, via a new
  picker next to the product selector. Available on archive volumes and any current/history-
  loaded frame; not yet available on the freshest still-arriving live frame.

### Changed
- The app's interface now uses a cleaner built-in font, with a bolder weight for headings and
  buttons. Map place labels are unaffected and still follow the font chosen in Settings.
- Correlation Coefficient now renders with its own color table (low correlation in browns/
  oranges for non-precipitation returns, blues approaching white near 1.0 for uniform
  precipitation) instead of the generic ramp shared with other secondary products.
- A product with no data in the current frame (e.g. dual-pol products on an older, pre-dual-pol
  volume) now shows grayed out in the product picker instead of being selectable to a blank view.

### Fixed
- In 2- and 4-pane layouts, each pane's product picker could render on top of the Settings and
  animation-export windows instead of behind them.
- Clutter Filter Power's data was silently dropped during frame compaction, so it never actually
  had anything to display even before today.
- Fixed the map briefly rendering blank and the app dropping frames when the UI scale was set
  smaller than 100%.
- The "Saved screenshot/animation to..." message now fades out on its own a few seconds after
  saving.
- The Windows app icon is now embedded in the executable, so it shows correctly in Explorer, the
  desktop shortcut, and the taskbar.

## [0.4.0] - 2026-09-26

### Added
- Copies installed from the Mac DMG or the Windows installer can now update themselves: choose
  **Update now** in Settings and FirstTilt downloads, installs, and restarts into the new version.
  Updates are signature-checked before installing. Updating from 0.3.0 still needs one manual
  download.
- The Mac installer now opens to a window where you drag FirstTilt into Applications.

### Changed
- "What's new" now opens automatically only after feature updates (minor or major versions), not
  after bug-fix updates. Every release's notes are still in Help → What's new.

## [0.3.0] - 2026-09-26

### Added
- Default radar site: right-click a site on the map or in the site list (or use Settings) to load
  it at startup.
- Favorite sites: star sites in the site list or from the map, reorder them in Settings, and press
  `[` / `]` to cycle through them.
- Help menu and window (F1) listing every mouse and keyboard control.
- In-app update check with a notice when a new version is available, plus "What's new" notes for
  each release.
- Minimum population slider for town labels.
- Alert detail cards: click an alert to pin a draggable card joined to it by a leader line. Cards
  show damage-threat and tornado tags, issue and expiry times (local and Zulu) with a live
  countdown, hail and wind, the towns inside the alert, and product IDs, with buttons to center the
  map and copy the details as text. Pin several at once; a card stays open (marked inactive) if
  its alert is cancelled or expires.

### Changed
- Esc no longer quits FirstTilt. It closes the top menu, window, or alert card, like other apps;
  quit with Cmd+Q on macOS, Alt+F4 on Windows, or the window's close button.
- New FirstTilt app icon and logo.
- Refreshed top and bottom bars with a consistent icon set and clearer active/hover states.
- Cleaner site list with search, a favorites section, and default/favorite markers.
- Mouse-wheel zoom now glides smoothly like trackpad zoom.
- Town labels no longer flicker while panning; they stay put and slide off the edge of the map.
- Hovering an alert now highlights its outline with a small label instead of a large fixed card.

### Fixed
- Live radar updates now add new frames to the timeline instead of replacing the latest one.
- Reflectivity no longer shows range-folding artifacts or a shortened range from the Doppler cut.
- The site list no longer scrolls visibly when opened.

## [0.2.2] - 2026-09-10

### Fixed
- Release packaging: checksums are generated reliably for every download.

## [0.2.1] - 2026-09-10

### Added
- Super-resolution radar data when available, with a setting to turn it off.
- Optional sweep animation when a new scan arrives.

### Changed
- macOS builds are signed and notarized.

## [0.2.0] - 2026-09-09

### Added
- Weather alerts and outlooks with per-alert styling.
- Basemap styling for coastlines, countries, states, and counties.
- Multi-pane layouts (1, 2, or 4 panes) with a product per pane.
- Screenshot and animation export (PNG, GIF, MP4).
- Real-time radar updates from the live Level II feed.

## [0.1.0] - 2026-08-22

### Added
- First release: native NEXRAD Level II radar viewer with settings, radar history, and installers
  for macOS and Windows.
