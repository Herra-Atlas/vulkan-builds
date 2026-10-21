# vulkan-builds

Prebuilt Windows binaries that ProjectZ downloads at runtime.

Nothing here is compiled by this repository. It holds the **notes** for each
build and, in the Releases tab, the archives themselves. That split is on
purpose: a zip is 47 MB, and committing one per rebuild would grow the
repository forever for files that are only ever used as downloads.

## Layout

```
builds/
├── whisper/     whisper.cpp with the Vulkan backend, plus parakeet-cli
└── parakeet/    reserved for a standalone parakeet build
```

Each folder has a `README.md` naming the release tag, the asset, and what the
archive contains. The app pins those names, so renaming an asset is a breaking
change to it.

## Naming

```
<project>-<backend>-<upstream revision>.zip
```

For example `whisper-vulkan-b5454.zip`. The revision is the whisper.cpp commit
tag the build came from — not ours — so a build can always be traced back to
the source it was made from.

## Publishing a build

1. Zip the contents of `build\bin` so the DLLs sit at the archive root.
2. Create a release whose tag is the file name without `.zip`, e.g.
   `whisper-vulkan-b5454`.
3. Attach the zip. GitHub publishes a SHA-256 for every asset; the app verifies
   it before unpacking, so a truncated or replaced upload is refused rather
   than installed.
4. Update the folder's `README.md` with the tag, size and hash.

## Why Vulkan

The Vulkan backend is the only one that keeps transcription on the GPU without
a CUDA install. The builds ship `ggml-cpu.dll` alongside it, so a machine with
no Vulkan device still runs — slower, not broken.
