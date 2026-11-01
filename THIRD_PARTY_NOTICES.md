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


Avalonia desktop dependencies (initial adoption 2026-10-30; paired release preparation 2026-11-01)
Avalonia 12.1.4, NativeWebView 12.1.1, MicroCom.Runtime 0.11.6 and
Tmds.DBus.Protocol 0.94.1 are MIT licensed. Avalonia.BuildServices 11.3.2 is a
build-only MIT component. ANGLE native package 2.1.27548.20260419 uses BSD terms.
SkiaSharp 3.119.4 and HarfBuzzSharp 8.3.1.3 include MIT wrappers and independently
licensed native material. Full supplier notices are retained, including BSD,
Apache-2.0, FreeType, PNG, JPEG, ICU and zlib terms and alternative-license texts.
Portions use the FreeType Project under its FTL alternative, with original
copyright credits in the complete notice. No change to vendor terms is implied.
The generic notice's libmicrohttpd entry belongs to an upstream tools-only target,
disabled in the selected SkiaSharp build graph, rather than a new media linkage.

Eligibility was reviewed before project adoption; exact package/source commits,
SHA-256/SHA-512 and offline license resources are in
docs/licensing/avalonia-dependency-review.json. Full license/notice texts are
embedded and individually discoverable in ? -> Third-party Licenses. The release
scope and exact-package eligibility are recorded separately from the original
development-adoption checkpoint. Every Windows/Ubuntu target must pass exact
bundle, runtime, resource/license and real startup checks before publication.
The desktop-runtime-manifest.json catalog identifies reviewed packages and their
license resources; it is not a claim that all files/other-RID assets in a package
are redistributed. No paid WebView package is adopted.

Linux system prerequisites
The Ubuntu executable includes its .NET/Avalonia application runtime but does not
redistribute Linux mpv, ffmpeg/ffprobe or a WebKit browser engine. These come from
the user's Ubuntu repositories and keep their own package versions, licenses,
copyright notices and source-package references under /usr/share/doc. They are
invoked as native external CLI/JSON-IPC processes; libmpv/libavcodec are not linked
into the managed application. The existing exact GPL binary/source-risk decision
above concerns the bundled Windows artifacts, not unidentified Linux binaries.

GTK 3 and WebKitGTK 4.1/libsoup 3 are replaceable system shared libraries. GTK and
relevant WebKit components use LGPL-2.1-or-later; WebKit also contains BSD-licensed
components. They are not copied into the application bundle or modified here.
Their applicable replacement, modification and debugging rights are preserved;
this private application source policy does not remove those rights. Full LGPL
2.1 text is included in LGPL-2.1.txt and the offline license catalog. Consult the
installed package copyright files for exact system component/source information.
Windows instead uses the separately installed WebView2 Evergreen system runtime.

SDK build-only dependency
Microsoft.NET.ILLink.Tasks 10.0.13 is an MIT-licensed .NET SDK build tool
restored by the single-file targets. It is not shipped in the runtime bundle;
trimming and Native AOT remain disabled. Its exact package and MIT/full .NET
third-party notices are recorded in the desktop review/catalog and offline
licenses. The package third-party notice bytes match the existing .NET 10.0.13
notice resource.
