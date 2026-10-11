# Third-party components

The free desktop edition preserves upstream attribution and bundled dependency notices. Corresponding application source is included and is also available at https://uncensorcloud.com/download/source.

- Jasna 0.6.0-alpha5: upstream LICENSE is AGPL-3.0; corresponding source is included in `source/upstream-jasna`. The restored 3.2 studio, motion pipeline and compatibility modifications are readable source in `studio`. Preserve the AGPL attribution and source obligations when distributing a derivative build.
- Lada generic restoration v1.2 weights: credited to the Lada Authors. The upstream weight-specific license declares AGPL-3.0: https://raw.githubusercontent.com/ladaapp/lada/main/model_weights/lada_mosaic_restoration_model_generic_v1.2.pth.license. The supplied file's SHA-256 is d404152576ce64fb5b2f315c03062709dac4f5f8548934866cd01c823c8104ee.
- Python 3.13.12 embeddable runtime: official Windows distribution. License is in `licenses/Python-LICENSE.txt` and `studio/runtime/LICENSE.txt`.
- Node.js 24.14.1: copied from this machine's installed runtime. License and bundled notices are included in `licenses/Node-LICENSE.txt`.
- FFmpeg, PyTorch, TorchVision, NVIDIA CUDA/TensorRT/NVENC/RTX dependencies and other Python packages are supplied by the user's existing engine. Their embedded license files and metadata are preserved under `engine/_internal`. They retain their individual licenses; the wrapper does not relicense them.

The package excludes the upstream executable's original sample videos, all service credentials, upload history, output history and local logs. One tested RF-DETR v6 detection engine cache is included with its GPU/runtime fingerprint; the app archives it before reuse when the device fingerprint changes. RF-DETR detection weights originate from Kruk2's Jasna releases (https://github.com/Kruk2/jasna/releases). The v6 large model is documented at https://github.com/Kruk2/jasna/blob/main/docs/en/models.md. These upstream files retain their original ownership and notices; uncensorcloud does not claim to own or relicense them.

## Offline subtitle components

- OpenAI Whisper large-v3-turbo and Meta M2M100 1.2B model weights: MIT. Attribution and licenses are in `studio/subtitle-licenses`; immutable upstream revisions and quantization are recorded in `studio/subtitle-models/manifest.json`.
- Faster Whisper, CTranslate2, Transformers, SentencePiece, OpenCC, PyAV, NumPy, ONNX Runtime and their dependencies retain their respective licenses, supplied in `studio/subtitle-runtime` package metadata/license directories. Package versions, Windows wheel hashes and license identifiers are recorded in `studio/subtitle-runtime-lock.json`.
- NVIDIA CUDA 12 cuBLAS and cuDNN 9 inference DLLs retain NVIDIA redistribution terms. Their wheel distribution notices and license metadata are preserved in `studio/subtitle-runtime`.
- Local subtitle source is provided in `studio/subtitle_worker.py`, `studio/subtitle_core.py`, `studio/local-subtitles.mjs` and the UI files, as well as the corresponding source download. Customer media, transcripts and private service/signing credentials are never bundled.
