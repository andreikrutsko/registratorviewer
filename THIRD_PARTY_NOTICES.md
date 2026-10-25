RegistratorViewer.Next — third-party software notices

Application source is maintained privately. This document does not grant an open-source license to the application's own code. The owner approved the current application distribution model on 2026-10-25.

mpv v0.41.0-1107-g36bf3d5290
Unmodified external playback process; Windows package dated 2026-10-08.
Project and license: https://github.com/mpv-player/mpv/blob/36bf3d5290/Copyright
Source: https://github.com/mpv-player/mpv/tree/36bf3d5290
Windows package/build recipes: https://github.com/shinchiro/mpv-winbuild-cmake/releases/tag/20261008
mpv's default license is GPL version 2 or later; its exact upstream Copyright notice and GPL-2.0/GPL-3.0 texts are embedded. It contains independently licensed libraries, including its FFmpeg snapshot N-127242-g5d4755f7d. Preserve upstream notices and corresponding-source obligations.

FFmpeg / ffprobe 9.0.2, Gyan essentials Windows build
Unmodified external utility processes, licensed GPL v3 by the binary distributor.
Binary/build information: https://www.gyan.dev/ffmpeg/builds/
Corresponding FFmpeg revision: https://github.com/FFmpeg/FFmpeg/commit/946fcce07b
Source and library licenses: https://ffmpeg.org/legal.html
The original distributor's build README and GPL-3.0 license text are embedded. GPL obligations for these components remain independent of the application's private source. A general upstream URL alone must not be treated as proof that all corresponding-source distribution obligations have been met.

d3dcompiler_47.dll — Microsoft proprietary component (shipped as d3dcompiler_43.dll)
Unmodified signed bytes distributed with the pinned mpv Windows package, SHA-256 4b074a3976399dc735484f5d43d04b519b7bdee8ac719d9ab8ed6bd4e6be0345. Normal-profile Windows inspection confirms Microsoft Corporation copyright, valid Microsoft Authenticode and version 10.0.18362.1. Its original/internal name is d3dcompiler_47.dll; the bytes exactly match Microsoft.Windows.SDK.CPP 10.0.18362.5, c/Redist/D3D/x64/d3dcompiler_47.dll. The distributor renamed the file without changing its bytes. The Windows SDK license and referenced redistribution list identify this unmodified compiler object code for Classic Windows apps, subject to their conditions. Full SDK terms are embedded. The owner approved this renamed/self-extracting delivery and the identified SDK conditions on 2026-10-25; no metadata waiver is required or applied. The earlier metadata-absence observation and the unrelated DXSDK compiler_43 comparison do not describe its actual origin. This is proprietary Microsoft software, not GPL/LGPL.
https://www.nuget.org/packages/Microsoft.Windows.SDK.CPP/10.0.18362.5
https://aka.ms/WinSDKLicenseURL
https://learn.microsoft.com/en-us/legal/windows-sdk/redist
WebView2 Evergreen is a separately installed Microsoft OS prerequisite.

Microsoft.Web.WebView2 SDK 1.0.4314.35
Microsoft license and third-party notice texts are embedded from the pinned SDK package.
https://www.nuget.org/packages/Microsoft.Web.WebView2/1.0.4314.35

MapLibre GL JS 6.15.0
BSD-3-Clause. Its license text is embedded from the pinned package.
https://github.com/maplibre/maplibre-gl-js

.NET / Windows Desktop 10.0.13 runtime
The self-contained publish profile pins 10.0.13. Its actual NuGet runtime-pack LICENSE.TXT, THIRD-PARTY-NOTICES.TXT and Windows Desktop LICENSE are embedded verbatim as offline resources and available in Third-party Licenses. They were not present as loose files in the previous bundle; explicit embedding repairs that omission.
https://github.com/dotnet/runtime/tree/v10.0.13
https://github.com/dotnet/windowsdesktop/tree/v10.0.13

Map data and online providers
MapLibre is a rendering library; map data is not bundled. Provider attribution is retained on the map. OpenFreeMap, VersaTiles, OpenStreetMap contributors and Google provide their own terms. A Google Maps key and its billing belong to the user.

Public distribution approval, 2026-10-25
The owner explicitly approved the exact native components, transitive review, separate-process and embedded-payload integration, first-party Lua/GLSL resources and complete distribution inventory for release. The owner reports checking Vulkan on clean Windows and accepts its remaining compatibility risk. Project approvalStatus, transitiveReview, integrationReview and artifact reviewStatus are APPROVED; distributionReview is COMPLETE. These are owner release decisions. Missing corresponding-source/build/patch evidence remains UNKNOWN under the explicit exception below; approval does not assert independent legal certification or complete source fulfillment.
The application invokes separate EXEs through CLI and JSON IPC; it does not link libmpv/FFmpeg APIs. Its Lua/GLSL resources execute within the media stack; this architecture was included in the owner's approval. Exact hashes, full licenses/notices, explicitly declared release assets and final artifact/publication checks remain required.

Owner source-material decision, 2026-10-25
The project owner explicitly accepted the risk of distributing the exact GPL media binaries without complete corresponding sources and build/patch materials, and removed that prerequisite from the project's release policy. Source completeness remains UNKNOWN; no complete corresponding-source archive is claimed or promised by this release. This owner decision does not amend third-party licenses or establish fulfillment of their conditions. Full licenses, notices, the exact manifest and all explicitly declared release assets remain required. The owner also approved the component/integration/distribution reviews; artifact and publication checks remain required. See correspondingSourcePolicy in media-tool-manifest.json for the hash-bound decision reference.
