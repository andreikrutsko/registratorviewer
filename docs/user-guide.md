# Quick start

Open MOV/MP4 recordings or a folder. Select a file or a compatible group to play it continuously. Click or drag the timeline/charts to seek; use the mouse wheel over that area to zoom. Details/F8 controls hover telemetry.

Set selection A and B to prepare a Cutting export. Video zoom, flips and pan are display settings and do not change the exported compressed video.

Double-click the video to enter video fullscreen; Escape returns. Choose a language in View → Language; no restart is needed.

The instrument cluster shows speed, current track distance, available recorded altitude, compass heading and acceleration. Missing values use dashes. Details/F8 also controls the instrument hover tooltips: altitude/distance/speed, compass direction and instantaneous X/Y/Z. Metric/British units apply to the instruments and their hover text together.

**View > Measurement** also updates file-list speed/distance captions and values,
charts, maps and hover text immediately. **View > Time Zone** changes displayed
file-list clocks and telemetry clocks while preserving the original recording
timestamps. Neither preference reparses or changes the recorded GPS/G-force.
Dragging the separators between video/sidebar, map/file list and video/timeline
saves their proportions. These choices persist in the user's home YAML file and
restore at the next launch, including at a different window size.

Map tools support pan, route seeking, measurement, fit and combined position/heading follow. A manual map pan suspends following; Recenter resumes it. Choose an open map provider or configure a user-owned Google Maps API key. Provider labels and attribution remain visible.

Select the ruler tool and click points on the map to measure a path. Each click
adds a ring in the measurement line's color. Each segment shows its length in
kilometers at its midpoint; the total uses your selected measurement system.
Undo removes the last point and segment, and Clear removes the measurement.

## Cutting and joining

Compatible video and audio are copied without re-encoding. If a stream cannot
be copied for the selected output, the application asks before re-encoding it
or exporting without it. Re-encoding takes longer and can change quality;
other compatible streams remain copied. Video recovery uses H.264 at the first
clip's frame size/rate, and audio recovery uses AAC. Ordinary playback never
converts the recording on disk.

In Cutting, an affected export checkbox is gray and disabled after this choice.
Use **Stream options** to change the decision. Absent streams are unavailable;
excluding video can create an audio-only file. Cancel leaves no completed output.
Copying video uses complete GOPs; explicitly re-encoded video follows source-frame
boundaries. Review the prepared range before starting.

Unexpected copy failures can offer a confirmed retry with re-encoding. The
application never switches to encoding silently. Retry can still fail, and
filesystem/access problems are reported separately.

## Copy, protect and delete recording files

The recording-list context menu and toolbar can copy selected recordings,
protect them with the file's read-only attribute, or move unlocked video files
to the system trash. Group commands apply to their member videos; a lock icon
also marks groups with only some protected members. Unlock removes that file
protection. Removing an entry from the list still leaves the file on disk.

**Copy File to Computer** selects a destination folder, copies video members
and associated GPS logs without re-encoding, and preserves modification times
within the destination filesystem's precision. Its progress window shows files,
bytes, percentage, elapsed time, speed and remaining time, with pause/resume,
cancel and Open Folder. Cancelling keeps completed copies and removes partial
outputs. Existing files require an explicit skip/replace choice; protected
outputs and source files cannot be overwritten. Copied recordings retain local
GPS source and correction settings when their complete group was copied.

**Delete File from Disk** operates on selected rows/groups. **Delete All
Unlocked Files from Disk** operates only on the loaded list. Both show the exact
video paths and count before moving files to trash. Protected videos and GPS
logs are retained. If trash is unavailable on a device, the file remains and an
error is reported; there is no automatic permanent-deletion fallback. Ubuntu
uses the desktop GIO trash service. Partial failures retain the remaining entries.

## GPS tracks and corrections

**Attach Track** opens timestamped GPX, TCX, FIT, NMEA, timed KML/KMZ,
GeoJSON, CSV/TSV, OziExplorer PLT and General LOG files. The application detects
content rather than trusting the filename extension. The preview shows time
intervals, usable points, segments and the route before saving a binding.
Original video, GPS logs and G-sensor samples remain unchanged. General LOG
files use the supported timestamped eleven-field A/V row profile, including
Mini 0806 recordings; the `.log` extension alone does not establish compatibility.

GPS preview dialogs have adjustable vertical panes: fields, compact information
and actions on the left, a full-height map on the right. The map uses the same
provider, units and controls as the main window. Coordinate corrections show
original geometry in gray and corrected geometry in red. Selecting a preview
point does not seek the video. Online map backgrounds need internet access;
GPS import, corrections and export remain available without a map connection.

Automatic companions match the complete filename stem, such as `clip.mp4`
and `clip.gpx`, even when the GPS file has a different extension. The Mini
0806 camera-letter naming rule is preserved. Initial detected-format priority
is GPX, TCX, FIT, NMEA, KML/KMZ, GeoJSON, CSV/TSV, PLT, then General LOG files.
**GPS tracks and source settings** can reorder formats, save that order for
new recordings, select a preferred external source, edit offsets, disable,
detach or relink files. Ambiguous equal-priority candidates require an
explicit choice.

**View > Current Coordinates > GPS source** retains **Built-in GPS** and
**Paired LOG**; Paired LOG now includes every supported external profile.
Automatic mode prefers valid native GPS. Explicit source selection persists
when that source is missing, without silently substituting native coordinates.
Gap filling from external tracks is a separate optional mode. External gaps
default to five seconds with no extrapolation; the established Mini/native
timing policy remains separate.

Explicit UTC timestamps retain their instants. Choose a source timezone or
fixed UTC offset for local timestamps. Ambiguous daylight-saving times need
an explicit offset; GGA-only NMEA needs a source date. A positive GPS offset
moves timestamps later: `+00:00:05` binds a 12:00:00 point to video time
12:00:05. If the video clock is unresolved, specify a reference video position,
date/time and timezone. Display timezone changes do not retime the binding.

CSV/TSV requires timestamp/latitude/longitude column mapping when the headers
are unfamiliar. Select the delimiter, decimal separator, encoding and time
format. Speed is in metres per second, altitude in metres and course in degrees.
ISO timestamps, explicit date/time patterns and `unix_s`/`unix_ms` are supported.
GeoJSON accepts time-bearing Points and LineString/MultiLineString arrays named
`timestamps_utc`, `coordTimes` or `times`, matching the coordinate arrays.
Untimed map geometry cannot be attached to video.

**View > Fix Coordinates** reflects longitude/latitude signs and shifts the
route in degrees/DMS or metres east/north. Reflections run before shifts.
Choose current-video or group scope in the correction dialog; direct menu
toggles apply to the group. Preview/reset is available. **Calculate Speed and
Heading Only by Coordinates** uses compatible consecutive valid positions,
without bridging gaps or inventing values for isolated points or duplicate
times. Normal mode prefers recorded speed/course. Saved corrections affect
the map, instruments, charts, statistics and GPS export; native video exports
retain original telemetry.

**Show Related GPS Log** opens the selected source with a paged normalized
table, original text/hex data, search and invalid-record filtering.
**Export Track** selects effective, original native or attached GPS and a
current-video, group, loaded-trip or A–B range. Output profiles are GPX 1.1,
KML, KMZ, GeoJSON, UTF-8 CSV, PLT and NMEA. Outages remain separate segments.
GPX carries optional motion/provenance extensions; other applications may
ignore them. NMEA loses altitude/accuracy/provenance, and PLT loses motion and
provenance. Format losses are reported. TCX/FIT/SRT output is deferred.

**File > Convert GPS Log** (`Ctrl+G`) works without video and supports single
or batch conversion with timezone, offset and correction settings. Each input
is detected separately; a malformed file does not stop the remaining batch.
Use separate batches for different CSV layouts. Source files cannot be
overwritten, existing destinations are protected and duplicate output names
are reported. Cancelling removes incomplete temporary output; completed files
from earlier batch items remain available.

## Video renderer

On Windows, choose **Settings > Renderer > Auto (Vulkan preferred)** or **Direct3D 11 (D3D11VA)**. Auto is the default and can try D3D11 once if Vulkan output initialization fails. Ubuntu uses the native Linux Auto renderer; D3D11 is unavailable. A change restarts only the video process, retaining the current position, pause/play, speed, audio, group, timeline, A-B loop and fullscreen/zoom/flips. Expect a short video interruption. The preference is saved for later sessions.

Open **Renderer diagnostics** in the same submenu to see the actual GPU context, decoder and mpv version. Vulkan rendering does not imply Vulkan hardware decoding; software decoding or `d3d11va-copy` can be valid. The supplied mpv retains its existing Windows loader/driver requirements: fallback cannot fix a missing DLL required to load the executable. No Vulkan SDK installer is included.

## New versions

RegistratorViewer.Next checks for a newer stable GitHub release once after startup. If one is available, confirm the prompt to open its release page in your browser. Choose **? → Check for new version** to check manually. Offline automatic checks stay silent; manual checks report network errors or temporary GitHub limits. The check never downloads or installs application files and does not send recording paths, GPS/G-force data or API keys.

## Camera groups

Front (A) and rear (B) recordings stay in separate groups, even when their times and codecs match. Manual grouping also rejects mixed A/B selections. Recognized recording metadata remains authoritative. When it is unavailable, supported timestamped filenames, including yyyy_MMdd_HHmmss, provide a fallback; the configured gap tolerance and stream compatibility checks still apply.

## GPS acquisition

If a recording starts before GPS fixation, its initial missing interval stays empty on the timeline. Invalid fixes also leave gaps in speed, map position and instruments. Cutting/joining preserves those media times and raw GPS blocks, including missing-fix status. Previously exported files with an incorrect old GPS timing archive are not repaired automatically; reopen the original recording and export again.
