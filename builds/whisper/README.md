# whisper — Vulkan build

whisper.cpp compiled with `-DGGML_VULKAN=ON`, Windows x64, MSVC.

## Release

| | |
|---|---|
| Tag | `whisper-vulkan-b5454` |
| Asset | `whisper-vulkan-b5454.zip` |
| Upstream | `ggml-org/whisper.cpp` @ `b5454` |
| Size | ~47.7 MB |

## Contents

Everything from `build\bin`, DLLs at the archive root:

| File | Purpose |
|---|---|
| `whisper-cli.exe` | transcribes a file |
| `whisper-server.exe` | HTTP server (unused by the app) |
| `parakeet-cli.exe` | Parakeet TDT models |
| `whisper-vad-speech-segments.exe` | voice activity detection |
| `whisper-quantize.exe`, `whisper-bench.exe` | tools |
| `ggml-vulkan.dll` | the GPU backend (39.6 MB, the bulk of the archive) |
| `ggml-cpu.dll` | fallback when no Vulkan device is present |
| `ggml-base.dll`, `ggml.dll` | tensor ops and backend loading |
| `whisper.dll` | whisper model code |
| `parakeet.dll` | Parakeet model code |

The DLLs must stay beside the executables — `ggml.dll` loads the backends from
its own directory.

## Parakeet ships in the same archive

`parakeet-cli` is an example inside whisper.cpp (`examples/parakeet-cli`), so it
comes out of the same CMake build. Splitting it into its own zip would duplicate
`ggml-vulkan.dll`, which is 39.6 MB of the 47.7.

**It is not `parakeet.cpp`.** This is whisper.cpp's own Parakeet TDT port and it
takes a ggml `.bin`, not a GGUF. A model converted for `mudler/parakeet.cpp`
will not load here.

Parakeet model (f16, ~1.2 GB):

```
ggml-org/parakeet-GGUF :: ggml-parakeet-tdt-0.6b-v3-f16.bin
```

## Whisper models

```
ggerganov/whisper.cpp :: ggml-<size>[-<lang>].bin
```

`ggml-tiny.en.bin` is 75 MB and is the smallest useful English model.
