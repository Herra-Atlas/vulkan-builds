# parakeet

Reserved for a **standalone** Parakeet build — `mudler/parakeet.cpp` or a future
whisper.cpp extraction that builds on its own.

Nothing is here yet, on purpose. `parakeet-cli` and `parakeet.dll` currently come
out of the whisper.cpp build in [`../whisper`](../whisper), which already ships
them; a second archive carrying the same 39.6 MB `ggml-vulkan.dll` would be
waste.

## When something belongs here

- A Parakeet build that does **not** come from whisper.cpp.
- A model format other than the ggml `.bin` whisper.cpp reads — for example a
  `parakeet.cpp` GGUF, which this app cannot load with the whisper engine.

If that happens, the folder gets its own release tag and asset, following the
naming in the root README.
