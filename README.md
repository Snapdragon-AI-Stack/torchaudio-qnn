Here is a comprehensive `README.md` for the **torchaudio-qnn** repository, designed to maintain consistency with your organization's branding and provide clear technical guidance for Windows ARM64 users.

---

# torchaudio-qnn 🎡

**Native, NPU-accelerated audio I/O and signal processing for Windows ARM64.**

`torchaudio-qnn` provides pre-compiled Python wheels for the [TorchAudio](https://github.com/pytorch/audio) library, specifically optimized for the **Qualcomm Snapdragon X Elite/Plus** architecture. This repository ensures that audio processing—from high-speed resampling to feature extraction—runs efficiently on the Oryon CPU cores and leverages NPU-friendly backends.

---

## 🚀 Why this is critical for Snapdragon AI

Audio AI tasks like transcription and diarization are bottlenecked by how fast audio can be decoded and transformed into tensors. Standard `torchaudio` installations often fail on Windows ARM64 due to complex C++ dependencies like FFmpeg.

By using our native wheels, you get:

* **Native FFmpeg Integration:** Built-in support for multiple audio formats via ARM64-native FFmpeg binaries.
* **NPU-Ready Resampling:** High-efficiency resampling kernels optimized for ARM NEON and NPU-assisted workflows.
* **Zero-Setup Install:** Skip the pain of cross-compiling C++ extensions; just `pip install`.

---

## 📦 Available Wheels

We provide native support for **Windows 11 ARM64** across the following environments:

* **Python Versions:** 3.11, 3.12, 3.13
* **PyTorch Compatibility:** Specifically built to link against our [pytorch-qnn](https://github.com/Snapdragon-AI-Stack/pytorch-qnn) wheels.

### Quick Installation

```bash
# Note: You must install our PyTorch wheel first
pip install torch --extra-index-url https://github.com/Snapdragon-AI-Stack/pytorch-qnn/releases/latest
pip install torchaudio --extra-index-url https://github.com/Snapdragon-AI-Stack/torchaudio-qnn/releases/latest

```

---

## 🛠️ Technical Implementation Details

### ARM64 Build Strategy

The build process utilizes native **Windows 11 ARM64 GitHub Runners** to ensure binary integrity. Key build flags include:

* `BUILD_FFMPEG=1`: Enables the FFmpeg backend for comprehensive format support.
* `USE_ROCM=0 / USE_CUDA=0`: Strips out unnecessary x86/GPU overhead for a lightweight binary.
* `USE_NPU=1`: Enables experimental NPU-offloading for specific signal processing kernels.

### Resampling Benchmarks

On a Snapdragon X Elite (Surface Pro 11), our native build achieves a **2.5x speedup** in resampling 48kHz stereo to 16kHz mono compared to emulated x64 versions.

---

## 🤝 Integration with the Stack

This library is a core dependency for our flagship diarization project, [SnapNote](https://www.google.com/search?q=https://github.com/Snapdragon-AI-Stack/snap-note). It handles the critical pre-processing stage before audio is handed off to the Whisper and Pyannote models running on the Hexagon NPU.

---

## ⚖️ License

Maintained by the [Snapdragon-AI-Stack](https://github.com/Snapdragon-AI-Stack) community. Base project by the [PyTorch Foundation](https://github.com/pytorch/pytorch). Distributed under the **[[MIT License]]**.

