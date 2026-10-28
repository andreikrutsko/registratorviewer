# Quick start

Open MOV/MP4 recordings or a folder. Select a file or a compatible group to play it continuously. Click or drag the timeline/charts to seek; use the mouse wheel over that area to zoom. Details/F8 controls hover telemetry.

Set selection A and B to prepare a Cutting export. Video zoom, flips and pan are display settings and do not change the exported compressed video.

Double-click the video to enter video fullscreen; Escape returns. Choose a language in View → Language; no restart is needed.

The instrument cluster shows speed, current track distance, available recorded altitude, compass heading and acceleration. Missing values use dashes. Details/F8 also controls the instrument hover tooltips: altitude/distance/speed, compass direction and instantaneous X/Y/Z. Metric/British units apply to the instruments and their hover text together.

Map tools support pan, route seeking, measurement, fit and combined position/heading follow. A manual map pan suspends following; Recenter resumes it. Choose an open map provider or configure a user-owned Google Maps API key. Provider labels and attribution remain visible.

## Video renderer

Choose **Settings > Renderer > Auto (Vulkan preferred)** or **Direct3D 11 (D3D11VA)**. Auto is the default and can try D3D11 once if Vulkan output initialization fails. A change restarts only the video process, retaining the current position, pause/play, speed, audio, group, timeline, A-B loop and fullscreen/zoom/flips. Expect a short video interruption. The preference is saved for later sessions.

Open **Renderer diagnostics** in the same submenu to see the actual GPU context, decoder and mpv version. Vulkan rendering does not imply Vulkan hardware decoding; software decoding or `d3d11va-copy` can be valid. The supplied mpv retains its existing Windows loader/driver requirements: fallback cannot fix a missing DLL required to load the executable. No Vulkan SDK installer is included.

## New versions

RegistratorViewer.Next checks for a newer stable GitHub release once after startup. If one is available, confirm the prompt to open its release page in your browser. Choose **? → Check for new version** to check manually. Offline automatic checks stay silent; manual checks report network errors or temporary GitHub limits. The check never downloads or installs application files and does not send recording paths, GPS/G-force data or API keys.

## Camera groups

Front (A) and rear (B) recordings stay in separate groups, even when their times and codecs match. Manual grouping also rejects mixed A/B selections. Recognized recording metadata remains authoritative. When it is unavailable, supported timestamped filenames, including yyyy_MMdd_HHmmss, provide a fallback; the configured gap tolerance and stream compatibility checks still apply.

## GPS acquisition

If a recording starts before GPS fixation, its initial missing interval stays empty on the timeline. Invalid fixes also leave gaps in speed, map position and instruments. Cutting/joining preserves those media times and raw GPS blocks, including missing-fix status. Previously exported files with an incorrect old GPS timing archive are not repaired automatically; reopen the original recording and export again.
