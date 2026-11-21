# Quick start

On macOS, the app has only an **ad hoc (technical) signature** and requires
manual permission at first launch. Before opening recordings, follow the
[macOS verification and launch instructions](run-unsigned-macos-app.md), including
**Privacy & Security > Open Anyway**. Runtime and media components are included.

Open supported MOV/MP4 or Hikvision MPEG-PS recordings, or a folder. Select a file or a compatible group to play it continuously. Click or drag the timeline/charts to seek; use the mouse wheel over that area to zoom. Details/F8 controls hover telemetry.

Wheel zoom keeps the timestamp under the pointer in place. The inspected chart
area stays visible during background position updates; seeking or starting
playback restores following of the playback cursor. With Loop A–B enabled,
the charts continue following the selected playback range.

Set selection A and B to prepare a Cutting export. Video zoom, flips and pan are display settings and do not change the exported compressed video.

Double-click the video to enter video fullscreen; Escape returns. Choose a language in View → Language; no restart is needed.

The instrument cluster shows speed, current track distance, available recorded altitude, compass heading and acceleration. Missing values use dashes. Details/F8 also controls the instrument hover tooltips: altitude/distance/speed, compass direction and instantaneous X/Y/Z. Metric/British units apply to the instruments and their hover text together.

Acceleration peak dots also show their values, including negative peaks on
signed axes. Speed charts label the maximum in each recording fragment without
adding dots; gaps in GPS data separate fragments. Labels follow the selected
units and language. Zooming preserves the original peak selection.

**View > Measurement** also updates file-list speed/distance captions and values,
charts, maps and hover text immediately. **View > Time Zone** changes displayed
file-list clocks and telemetry clocks while preserving the original recording
timestamps. Neither preference reparses or changes the recorded GPS/G-force.
Dragging the separators between video/sidebar, map/file list and video/timeline
saves their proportions. These choices persist in the user's home YAML file and
restore at the next launch, including at a different window size.

Drag the right edge of a recording-list column heading to change its width.
The headings and recording rows stay aligned, and your column widths are
restored at the next launch. Resizing does not select, open or sort a recording.

Map tools support pan, route seeking, measurement, fit and combined position/heading follow. A manual map pan suspends following; Recenter resumes it. Choose an open map provider or configure a user-owned Google Maps API key. Provider labels and attribution remain visible.

Select the ruler tool and click points on the map to measure a path. Each click
adds a ring in the measurement line's color. Each segment shows its length in
kilometers at its midpoint; the total uses your selected measurement system.
Undo removes the last point and segment, and Clear removes the measurement.

## External storage and recursive discovery

Opening a folder searches its accessible subfolders as well. Names and filename
extensions do not determine whether a recording or GPS log is recognized. Logs
in another folder on the scanned volume can be paired by their matching basename;
General LOG camera-letter pairing remains supported.

Launching the app from an external USB SSD, flash drive or memory card starts a
scan of that volume. For other connected external volumes, choose Yes or No in
the notification at the top. **File > Scan connected storage** lets you select a
volume yourself, including an internal disk. Internal disks are scanned only
with your consent.

Found recordings are added to the current list while playback continues. Enabled
automatic grouping applies; manual groups and A/B selections are retained. The
progress bar shows discovery and analysis, and **Cancel discovery** stops finding
more files. A small device profile remembers successfully recognized formats for
later scans; each file is still checked. An unplugged device stops its playback.
Scan a reconnected device again before using entries from its earlier connection.

## Background file analysis

A progress bar at the top remains visible while recordings are being analyzed.
Playback, navigation and the main menu remain available. Commands that need the
completed analysis display a message explaining when they will be available.
Clear File List stops playback and clears the video as well as the recording list.

Hikvision H.265/HEVC IPCAMs (MPEG-PS) are recognized by their contents, including
Program Stream files named with an MP4 extension. Use MOV to retain their native
mu-law audio without conversion. Recorded audio delays remain unchanged.

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
protect them with native read-only attributes or write permissions, or move unlocked video files
to the system trash. Group commands apply to their member videos; a lock icon
also marks groups with only some protected members. Unlock removes that file
protection, restoring the original write permissions where available. Associated GPS logs are protected too. Removing an entry from the list still leaves the file on disk.

**Copy File to Computer** selects a destination folder, copies video members
and associated GPS logs without re-encoding, and preserves modification times
within the destination filesystem's precision. Its progress window shows files,
bytes, percentage, elapsed time, speed and remaining time, with pause/resume,
cancel and Open Folder, while the main player remains usable. Filesystem failures offer applicable retry, skip and cancel actions. Unsupported metadata is reported separately from a successful data copy. Cancelling keeps completed copies and removes partial
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
GeoJSON, CSV/TSV, OziExplorer PLT, General LOG files and 70mai GPSData V02 journals. The application detects
content rather than trusting the filename extension. The preview shows time
intervals, usable points, segments and the route before saving a binding.
Original video, GPS logs and G-sensor samples remain unchanged. General LOG
files use the supported timestamped eleven-field A/V row profile, including
Mini 0806 recordings; the `.log` extension alone does not establish compatibility.

### 70mai GPSData V02

Keep the shared `GPSData*.txt` journals together with your recordings. You can
open a full memory-card copy, a partial Front/Rear copy, a flat folder, or one
video with its original name. The app looks for a matching journal in the
video's folder and its parent folders. Multiple journals are supported; the
`$V02` contents and complete video identity establish the association. Normal,
Event, Parking and Lapse folder names are not required. Smaller `.s_Front`
copies are omitted during folder scans; you can still open one explicitly.

Use **Attach Track** when the journal is stored separately. Existing GPS source
settings let you select built-in or external coordinates and adjust the time
offset. The initial interval before GPS acquisition stays empty. Recorder clock
alignment is estimated from video identities; it is not proof of absolute UTC.
Check the preview and use a verified recording time/manual offset if the clocks
are uncertain. Use **Refresh File List** after replacing or updating a journal.

The route includes recorded speed and course. Uncalibrated acceleration counts
are retained in the source information and saved video telemetry, without being
displayed as physical g. Saving a fragment or joining files includes only the
selected telemetry in the saved video's RV telemetry archive. Renamed outputs
reopen with their route; the shared original journal is not rewritten or copied
wholesale. GPS tracks can also be exported in the existing output formats.

### Preview and source selection

GPS preview dialogs have adjustable vertical panes: fields, compact information
and actions on the left, a full-height map on the right. The map uses the same
provider, units and controls as the main window. Coordinate corrections show
original geometry in gray and corrected geometry in red. Selecting a preview
point does not seek the video. Online map backgrounds need internet access;
GPS import, corrections and export remain available without a map connection.

Automatic companions match the complete filename stem, such as `clip.mp4`
and `clip.gpx`, even when the GPS file has a different extension. The Mini
0806 camera-letter naming rule is preserved. Initial detected-format priority
is GPX, TCX, FIT, NMEA, KML/KMZ, GeoJSON, CSV/TSV, PLT, General LOG files, then 70mai GPSData V02.
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
route in degrees/DMS or metres east/north. **Shift coordinates** opens one dialog
for both axes. Select **Coordinate shift units** first: angular fields are
editable in Degrees/DMS mode, and East/North fields in Metres mode. Inactive
values are retained when switching units. Negative East/North values shift west
or south. Reflections run before shifts.
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

Automatic grouping allows gaps of up to **60 seconds** by default for every
supported recording type and camera model. Source timestamps and gaps remain
on the timeline. Adjust the allowance in **Find Groups Automatically**; disabling
automatic grouping and explicit manual ungrouping remain respected.

Front (A) and rear (B) recordings stay in separate groups, even when their times and codecs match. Manual grouping also rejects mixed A/B selections. Recognized recording metadata remains authoritative. When it is unavailable, supported timestamped filenames, including yyyy_MMdd_HHmmss, provide a fallback; the configured gap tolerance and stream compatibility checks still apply.

## Multicamera playback

With automatic grouping enabled, recordings with matching camera identities
and confirmed common recording times appear in an expandable **Multicamera**
section. Consecutive recordings are grouped within each camera first. Expand
the section to see those camera groups; selecting a child plays that camera
alone. Selecting the section plays its cameras together and preserves the
current recording time and playback state when switching between these views.

Two cameras use top and bottom panes. Three or four cameras use a four-pane
layout, with an empty black pane for three cameras. Drag the dividers to change
the proportions. Video keeps its aspect ratio. Wheel zoom and dragging apply
to the camera under the pointer; video zoom commands in the top menu apply to
all panes.

The camera supplying sound has a thin green outline. Click another camera to
select its sound. GPS, charts and the timeline remain shared. If one camera has
no recording at the current time, only its pane becomes black. Playback skips
an interval automatically when all cameras are missing; only those common gaps
are marked on the shared timeline.

Cutting and joining a selected section opens the existing export workflow for
each camera in sequence. Each output keeps that camera's compressed streams
unless you explicitly choose conversion in an incompatibility dialog.

## GPS acquisition

If a recording starts before GPS fixation, its initial missing interval stays empty on the timeline. Invalid fixes also leave gaps in speed, map position and instruments. Cutting/joining preserves those media times and raw GPS blocks, including missing-fix status. Previously exported files with an incorrect old GPS timing archive are not repaired automatically; reopen the original recording and export again.
