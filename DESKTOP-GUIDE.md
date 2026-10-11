# uncensorcloud 3.5.0

A free portable Windows video restoration edition. Processing runs on your own GPU. The optional cloud workspace at https://uncensorcloud.com/workspace provides an RTX 5090 preview and paid full-video processing.

## Getting started

1. Extract the entire ZIP into a writable folder. Do not run it inside the archive.
2. Double-click `Start-Free.cmd`. The development folder also includes `Start-Web.cmd` for the local web preview.
3. Your browser opens automatically. Create a free account or sign in on uncensorcloud.com, confirm the desktop code, and allow this desktop. No payment card is required. After sign-in, the free edition checks your computer and runs a short synthetic 1080p / 30fps benchmark to estimate the time needed for a one-hour video. You can stop the benchmark. Starting a video task stops it first.
4. Import a short clip and draw a restoration region. Add corrections along the timeline when following motion.
5. Choose temporal stability, output quality and memory settings. Generate a 10-second preview in the panel at the top: automatic mode finds a mosaic region; manual tracking starts at the first correction, and fixed mode uses the selected timeline time. Compare the result, then process the full video and download it with the report.
6. Closing the browser does not stop processing. Finish or cancel the current task, then use `Stop-Free.cmd` or, for the web preview, `Stop-Web.cmd`.

Imported copies and task records are stored in `studio/data` (free edition) or `studio/data-web` (web preview). Results are stored in `studio/outputs` or `studio/outputs-web`. Source files are never overwritten. Files are not automatically deleted; you can clean up these folders when you no longer need them.

## Account access and optional support

Free Desktop requires a verified account and an internet connection. The app verifies desktop access every 30 seconds; each authorization lasts at most 45 seconds. Administrators can pause desktop access independently of cloud access. A failed account check stops previews, processing and benchmarks. Your local video files are preserved. A desktop session lasts up to 30 days and is stored with Windows user-bound DPAPI encryption. Signing out or resetting your password ends the relevant desktop sessions.

Older offline releases must be updated to use account access. This managed client is not a tamperproof licensing system; the corresponding source remains available under its license.

The optional tip jar at https://uncensorcloud.com/support accepts one-time support through Stripe. Tips do not buy processing minutes or change account permissions. Advertisement spaces are reserved for future sponsors; no advertising tracker is included.


## Offline subtitles (new in 3.5)

Import and select a video, then click **Open offline subtitles**. Choose the spoken language, output language and audio track. Start with **Try 30-second subtitles** at a time where dialogue is audible. **Generate full-video subtitles** processes the complete audio independently of mosaic detection or restoration regions.

Original-language transcription and eight output languages are available: English, Simplified Chinese, Traditional Chinese, Japanese, Korean, Spanish, Portuguese and Arabic. Whisper large-v3-turbo and M2M100 1.2B converted models are included; no model downloads or external text API are used during inference. Videos and transcripts stay on this computer. An internet connection is still needed for the existing account verification.

**Auto** tries the independent CUDA-12 subtitle runtime, then CPU if GPU speech inference is unavailable. **CPU** can run subtitles when this computer cannot run video restoration. Subtitle generation, restoration, preview, exports and benchmarks share one processing queue. Cancel a job before starting another. Each subtitle job loads its speech model once and processes bounded audio windows; translation loads once per job. Model loads across separate jobs are not cached in a permanent background GPU process.

Review the video with captions, edit cue times and text, then **Save edits**. Saves publish a complete revision atomically; a stale editor cannot overwrite a newer revision. SRT, VTT and original-language SRT exports are available. **Export captioned video** adds a switchable subtitle track to the restored output if restoration has finished, otherwise to the imported original. Video and all audio tracks are copied without re-encoding. MKV preserves the broadest codec range; MP4 requires a compatible video and audio codec. Preview generation produces captions only for the sampled range, so generate the full video for a complete subtitle export.

Generated cues are wrapped to two lines where possible, with reading-speed warnings. Speech recognition and translation are estimates: review names, multilingual audio, accents and noisy recordings. Leading silence is preserved. Silent audio produces no captions. The first audio track is not always the dialogue track; select another track when needed. Current limits: eight hours per video, 12,000 cues and 500,000 text characters. Generating again preserves previous job folders and exported videos. Interrupted jobs can be retried; subtitle inference is restarted, not resumed mid-window.

The package includes approximately 2 GB of subtitle model weights plus Windows inference libraries. Keep sufficient disk space for extraction, imported copies, generated audio and separate outputs. **Subtitles are free and processed locally.** Cloud subtitle pricing remains separate.

## System requirements and supported features

- Windows 10/11 x64, a modern NVIDIA GPU, and a driver compatible with CUDA 13. Development verification used an RTX 4090 Laptop with 16GB VRAM; other GPUs have not all been tested.
- Node.js, Python and engine dependencies are bundled. Your computer supplies the GPU driver.
- Basic compatibility checks run real CUDA computation and HEVC NVENC encoding, and check Windows x64, model files and at least 2GB temporary disk space. Passing these checks does not guarantee that every resolution and setting will fit. The speed benchmark also runs the restoration model.
- Recommended for long videos: 16GB VRAM, 32GB system RAM, 8 logical CPU cores and 50GB available disk space. These are recommendations, not artificial minimum requirements. Lower-spec computers can still try the 30-frame memory profile and a short clip.
- Includes RF-DETR v6 automatic detection and manual regions, motion tracking, fixed regions, timeline corrections, scene-cut resets, temporal stability and region enhancement. Automatic detection depends on the model’s training coverage. If no region is found, the app reports it and you can switch to manual selection.
- Input requires even dimensions, SDR and 8-bit video. Full output is HEVC / MP4 with original dimensions and audio. Browser previews and synchronized comparisons use H.264 and show up to 10 seconds starting at the first restored region; video downloads contain the full HEVC output.
- Reconstructed details are model estimates and cannot guarantee recovery of original information. The bundled example is a synthetic, non-person chart, not customer footage.
- Both editions can be open together. Process tasks sequentially on the same GPU to avoid competing for VRAM.
- The launcher uses a temporary drive alias so native dependencies work from folders with Unicode characters or spaces. It does not move files or change GPU driver settings.
- A verified detection engine cache is included. Changing GPU, driver or runtime archives an incompatible cache. The first automatic task may need several minutes to rebuild it; keep the background service running.

## Device checks and one-hour estimates

- The free edition shows GPU / VRAM, system RAM, logical CPU cores and free space on the working drive. These readings and benchmark results stay on your computer.
- Choose 720p / 1080p / 4K, 24 / 30 / 60fps, manual or automatic mode, stability, enhancement and a 30 / 60 / 90-frame memory profile. Each configuration needs its own measurement. Without one, the app shows “No measured estimate yet.” Benchmark settings do not change the processing settings of your clips.
- The benchmark generates 180 SDR 8-bit frames locally and runs the production restoration and HEVC encoding pipeline. One fixed region covers about 16% of the frame, and every frame is restored. Automatic mode also runs real detection, then uses the fixed reference region to prevent empty detections from producing misleading speed results.
- The first 30 frames warm up the pipeline; the remaining 150 frames measure throughput after encoding. Estimated time is `3600 × video frame rate ÷ measured processing fps + loading and first-frame overhead`. Synthetic video generation and initial detection-engine compilation are excluded from sustained processing speed.
- The displayed scenario range is 0.7–1.8 times sustained processing time. It is not a statistical confidence interval or a completion-time promise. Multiple regions, tracking, content, encoding, audio, temperature, disk speed and other applications affect actual duration; long videos can exceed the range. Evaluate your own representative short clip first.
- Measurements are cached in `studio/data/benchmark-cache.json`, matching GPU, driver, runtime, CPU, RAM, OS, model contents and benchmark version. Changed conditions invalidate the cache. Even unchanged hardware can perform differently with power or temperature changes; use Run benchmark again to refresh it.
- Failed basic checks, hardware below the long-video recommendation, or an estimated one-hour sample taking more than two hours trigger a suggestion to consider cloud processing. The cloud link opens https://uncensorcloud.com/workspace in a separate tab. Sign in and choose a video there to get a free 10-second preview and a quote before paying. Local files and device measurements are not uploaded automatically; no unmeasured cloud speed is promised.

## Source and third-party components

The UI, server and compatibility layer are readable source in `studio`. Corresponding upstream engine source is in `source/upstream-jasna`; the development baseline commit is recorded in `product-source-commit.txt`.

Engine derivatives retain the AGPL-3.0 license; see `licenses/AGPL-3.0.txt` and `THIRD-PARTY-NOTICES.md`. Runtimes and model weights retain their individual licenses and notices. Corresponding application source is also available at https://uncensorcloud.com/download/source.

Supported input containers: MP4, M4V, MKV, MOV, WebM, AVI, TS, MTS, M2TS, M2T, MPEG, MPG, MPE, VOB, WMV, ASF, FLV, OGV, OGG video, 3GP, 3G2 and MXF. A readable video stream is required; playlists and audio-only files are not video inputs. The bundled decoder checks actual codec support. The frame editor and 10-second H.264 preview work independently of browser source-container playback.

## Official release verification

Official 3.5.0 releases include an Ed25519-signed file manifest. Startup checks shipped files before opening the workspace; this may take longer on a hard drive. Run `Verify-Release.cmd` to check manually. GPU engine/device caches, account state and user videos remain mutable. Keys and the current ZIP hash are available at https://uncensorcloud.com/api/desktop/release.

Account leases are signed, request/session bound and valid for at most 45 seconds. Private signing keys are never included. These checks authenticate official files and service responses; they do not prevent a modified client from replacing its verifier or prohibit AGPL-compliant forks. See `BRAND-NOTICE.md` and the corresponding source `cloud/DESKTOP-PROTECTION.md` for boundaries and modified-build instructions. This signature is not a Windows Authenticode publisher certificate.

## Building the subtitle bundle from source

Use an isolated build Python environment with PyTorch, Transformers and CTranslate2, then run `python scripts/prepare-subtitle-assets.py` to obtain the pinned upstream inputs. Convert each model with `SOURCE_MODELS` set to `.cache/subtitle-build/models` and `SUBTITLE_MODELS_OUTPUT` set to `.cache/subtitle-compiled`, using `python cloud/gpu/subtitle_models.py`. Do not change the pinned revisions in `cloud/gpu/subtitle-model-lock.json` without revalidation.

Download Windows Python 3.13 wheels with `python -m pip download --dest .cache/subtitle-windows-core-wheels --only-binary=:all: --platform win_amd64 --python-version 313 --implementation cp --abi cp313 faster-whisper==1.2.1 ctranslate2==4.8.2 transformers==4.51.3 sentencepiece==0.2.1 opencc-python-reimplemented==0.1.7 numpy==2.3.3 onnxruntime==1.23.2 av==16.1.0 huggingface-hub==0.36.2 tokenizers==0.21.4`. Download `nvidia-cublas-cu12==12.8.4.1` and `nvidia-cudnn-cu12==9.7.1.26` into `.cache/subtitle-windows-wheels` with the same platform options. Resolve exact dependency versions against `studio/subtitle-runtime-lock.json`; empty the build wheel directory when changing versions so multiple versions cannot overwrite one another.

Run `python scripts/prepare-desktop-subtitles.py` to hash-check and stage the offline Windows runtime and models. The official ZIP signs every shipped file. Publisher private signing keys are intentionally absent from corresponding source; modified builds retain the source-build label and existing account requirements.
