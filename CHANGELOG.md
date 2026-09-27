# Changelog

All notable changes to FirstTilt are listed here. This file is the public release notes: each
version's section is published with its release on
[FirstTilt-Releases](https://github.com/WoolawayWx/FirstTilt-Releases/releases) and shown in the
app's "What's new" window, so write entries for people using the app, not for the code.

Add notes under **Unreleased** as you work. `cargo xtask release <patch|minor|major>` moves them
under the new version when you release.

## [Unreleased]

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
