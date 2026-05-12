# 🦜 phuonganh-tts — Vietnamese TTS Studio

> **phuonganh-tts** is a Vietnamese Text-to-Speech model with instant voice cloning and bilingual support.
> This package includes local model weights for offline operation.

[![Awesome](https://img.shields.io/badge/Awesome-NLP-green?logo=github)](https://github.com/keon/awesome-nlp)
[![Model](https://img.shields.io/badge/Model-phuonganh--tts--v2-blue)](https://huggingface.co/phuonganh/phuonganh-tts-v2)

---

## Key Features

- **Offline-first** — Local model weights included; no internet required
- **Voice cloning** — Clone any voice with 3–5 seconds of reference audio
- **Multi-speaker conversations** — Built-in podcast and dialogue mode
- **Clean state management** — No global mutable state; stable under repeated requests

[![Awesome](https://img.shields.io/badge/Awesome-NLP-green?logo=github)](https://github.com/keon/awesome-nlp)
[![Discord](https://img.shields.io/badge/Discord-Join%20Us-5865F2?logo=discord&logoColor=white)](https://discord.gg/yJt8kzjzWZ)

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1b9PO-lcGZX9pEkEwQmu8MfhSnjxKrALW?usp=sharing)
[![Hugging Face phuonganh-tts-v2](https://img.shields.io/badge/%F0%9F%A4%97%20Hugging%20Face-v2-blue)](https://huggingface.co/Nemmer/phuonganh-tts-v2)
[![Hugging Face phuonganh-tts](https://img.shields.io/badge/%F0%9F%A4%97%20Hugging%20Face-v1-orange)](https://huggingface.co/Nemmer/phuonganh-tts-v2)


**phuonganh-tts-v2** is the next generation of on-device Vietnamese TTS, featuring **10,000+ hours** of bilingual training, **instant voice cloning**, and a dedicated **Podcast/Conversation** mode.

> [!IMPORTANT]
> **🚀 phuonganh-tts-v2 is here!**
> The full high-fidelity bilingual architecture is now available with:
> - **500+ Hours of Data:** Unmatched naturalness in both English and Vietnamese.
> - **Podcast & Dialogue Mode:** Multi-speaker support with emotional nuances.
> - **Zero-shot Cloning:** Clone any voice in 3-5 seconds across all v2 variants.

## ✨ Key Features (phuonganh-tts)

- **Auto-load on startup** — `phuonganh-tts-v2 (GPU)` loads automatically when GPU is available
- **GPU-optimized** — Uses LMDeploy on NVIDIA CUDA, Apple Metal, or Intel Arc XPU
- **Voice cloning** — Clone any voice with 3–5 seconds of reference audio
- **Multi-speaker conversations** — Built-in podcast and dialogue mode
- **Cache-first loading** — Skips re-download if the model is already cached
- **Clean state management** — No global mutable state; stable under repeated requests

---

## 🚀 phuonganh-tts Web UI

### Quick Start

```bash
# Clone the repo
https://github.com/mvu696841111/PhuongAnh-TTS.git
cd phuonganh-tts

# Install dependencies (GPU mode)
uv sync --group gpu

# Start the phuonganh-tts UI (auto-loads phuonganh-tts-v2 GPU)
uv run phuonganh-web

# Or use the standard entry point
uv run phuonganh-tts-web
```

The app opens at `http://127.0.0.1:7860`. `phuonganh-tts-v2 (GPU)` loads automatically.

## 📌 Table of Contents

1. [🦜 Installation & Web UI](#installation)
2. [📦 Using the Python SDK](#sdk)
3. [🐳 High-Quality Server (Standard Mode)](#docker-remote)
4. [🔬 Model Overview](#backbones)
5. [🚀 Roadmap](#roadmap)
6. [🤝 Support & Contact](#support)
7. [📑 Citation](#citation)

---

## 🦜 1. Installation & Web UI <a name="installation"></a>

### Setup with `uv` (Recommended)
`uv` is the fastest way to manage dependencies. 
```bash
# Windows:
powershell -c "irm https://astral.sh/uv/install.ps1 | iex"

# Linux/macOS:
curl -LsSf https://astral.sh/uv/install.sh | sh
```

1. **Clone the Repo:**
   ```bash
   git clone https://github.com/mvu696841111/PhuongAnh-TTS.git
   cd phuonganh-tts
   ```

2. **Install Dependencies:**
   - **Option 1: Minimal (Turbo/CPU)** - Fast & Lightweight
     > ⚠️ *Note: This mode only supports **phuonganh-tts-v2-Turbo (CPU)** — runs on any machine without a GPU, but **audio quality is lower** than Standard phuonganh-tts (especially for short phrases < 5 words). Recommended for quick testing or deployment on low-end devices.*
     ```bash
     uv sync
     ```
   - **Option 2: Full (GPU/Standard)** - High Quality & Podcast Mode *(For GPU users)*
     > 💡 *Note: Requires a CUDA-compatible NVIDIA GPU (CUDA version >= 12.8) or Apple Silicon MPS. [NVIDIA Toolkit](https://developer.nvidia.com/cuda-downloads) is required for maximum speed. Enables the full **phuonganh-tts-v2** backbone for maximum audio quality and high-fidelity voice cloning.*

     ```bash
     uv sync --group gpu
     ```

3. **Start the Web UI:**
   ```bash
   uv run phuonganh-tts-web
   ```
   Access the UI at `http://127.0.0.1:7860`.

---

## 📦 2. Using the Python SDK (phuonganh-tts) <a name="sdk"></a>

The `phuonganh-tts` SDK defaults to **Standard mode** (phuonganh-tts-v2 GGUF + ONNX) when used locally, providing a perfect balance of high audio quality and real-time performance on any CPU or GPU.

### Quick Start
```bash
# Minimal installation (Builds llama-cpp from source - may take a while)
pip install phuonganh-tts

# Optional: For Windows users (CPU pre-built)
pip install phuonganh-tts

# Optional: For macOS users (ARM64/Apple Silicon - Enables Metal GPU acceleration)
pip install phuonganh-tts --extra-index-url https://abetlen.github.io/llama-cpp-python/whl/metal/
```

```python
from phuonganh_tts import PhuongAnh

# Initialize in Standard mode (Default - Highest quality)
tts = PhuongAnh(emotion="natural") # emotion="natural" (giọng tự nhiên - mặc định) hoặc "storytelling" (giọng kể chuyện)

# 1. Simple synthesis (uses default Northern Female voice 'Trúc Ly')
text = "Chào bạn. Tôi là phuonganh-tts, tôi có thể giúp bạn đọc sách, làm chatbot thời gian thực, thậm chí clone giọng nói của bạn."
audio = tts.infer(text=text)

# Save to file
tts.save(audio, "output_Trúc Ly.wav")
print("💾 Saved to output_Trúc Ly.wav")

# 2. Using a specific Preset Voice
voices = tts.list_preset_voices()
for desc, voice_id in voices:
    print(f"Voice: {desc} (ID: {voice_id})")

my_voice_id = voices[1][1] if len(voices) > 1 else voices[0][1] # Giọng Tuyên
voice_data = tts.get_preset_voice(my_voice_id)

audio_custom = tts.infer(text="Tôi đang nói bằng giọng của Bác sĩ Tuyên.", voice=voice_data)

# 3. Save to file
tts.save(audio_custom, "output_Tuyen.wav")
print("💾 Saved to output_Tuyen.wav")
```

### 🚀 Turbo Mode (Bilingual & Extreme Speed)
Use `mode="turbo"` for the fastest possible inference, especially optimized for real-time English-Vietnamese code-switching.
> [!WARNING]
> Turbo Mode has lower audio quality compared to other modes and may produce artifacts or errors for very short sentences.


```python
from phuonganh_tts import PhuongAnh

# Initialize in Turbo mode (v2-Turbo GGUF)
tts = PhuongAnh(mode="turbo")

# Turbo v2 supports natural English-Vietnamese transitions
text = "Hệ thống điện chủ yếu sử dụng alternating current because it is more efficient."
audio = tts.infer(text=text)

tts.save(audio, "turbo_output.wav")
```

### 🦜 Zero-shot Voice Cloning (SDK) <a name="cloning"></a>
Clone any voice with only **3-5 seconds** of audio. 

> [!TIP]
> **Turbo mode** is recommended for voice cloning as it doesn't require reference text, while **Standard mode** (default) requires providing the `ref_text` for higher accuracy.

```python
from phuonganh_tts import PhuongAnh

# We'll use turbo mode for easy zero-shot cloning (no ref_text needed)
tts = PhuongAnh(mode="turbo")

# 1. Encode the reference audio (3-5 seconds recommended)
my_voice = tts.encode_reference("examples/audio_ref/example.wav")

# 2. Synthesize with the cloned voice
audio = tts.infer(
    text="Đây là giọng nói được clone trực tiếp bằng SDK của phuonganh-tts.", 
    voice=my_voice
)

tts.save(audio, "cloned_voice.wav")
```

---

## 🐳 3. High-Quality Server (Standard Mode) <a name="docker-remote"></a>

Deploy phuonganh-tts as a high-performance API Server (powered by LMDeploy) with a single command.

### 1. Run with Docker (Recommended)

**Requirement**: [NVIDIA Container Toolkit](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/latest/install-guide.html) is required for GPU support.

**Start the Server with a Public Tunnel (No port forwarding needed):**
```bash
docker run --gpus all -p 23333:23333 -v huggingface_cache:/root/.cache/huggingface ghcr.io/mvu696841111/phuonganh-tts:latest --tunnel
```

*   **Default**: The server loads the `phuonganh-tts-v2` model for maximum quality.
*   **Tunneling**: The Docker image includes a built-in `bore` tunnel. Check the container logs to find your public address (e.g., `bore.pub:31631`).

### 2. Using the SDK (Remote Mode)

Once the server is running, you can connect from anywhere (Colab, Web Apps, etc.) without loading heavy models locally.

**Installation**:
```bash
pip install "phuonganh-tts[gpu]"
```

**Usage**:
```python
from phuonganh_tts import PhuongAnh
import os

# Configuration
REMOTE_API_BASE = 'http://your-server-ip:23333/v1'  # Or bore tunnel URL
REMOTE_MODEL_ID = "phuonganh/phuonganh-tts-v2"

# Initialization (LIGHTWEIGHT - only loads small codec locally)
# Default emotion is "natural" (conversational) - set emotion="storytelling" for storytelling mode
tts = PhuongAnh(mode='remote', api_base=REMOTE_API_BASE, model_name=REMOTE_MODEL_ID, emotion="natural")
os.makedirs("outputs", exist_ok=True)

# List remote voices
available_voices = tts.list_preset_voices()
for desc, name in available_voices:
    print(f"   - {desc} (ID: {name})")

# Use specific voice (dynamically select second voice)
if available_voices:
    _, my_voice_id = available_voices[1]
    voice_data = tts.get_preset_voice(my_voice_id)
    audio_spec = tts.infer(text="Chào bạn, tôi đang nói bằng giọng của bác sĩ Tuyên.", voice=voice_data)
    tts.save(audio_spec, f"outputs/remote_{my_voice_id}.wav")
    print(f"💾 Saved synthesis to: outputs/remote_{my_voice_id}.wav")

# Standard synthesis (uses default voice)
text_input = "Chế độ remote giúp tích hợp phuonganh-tts vào ứng dụng Web hoặc App cực nhanh mà không cần GPU tại máy khách."
audio = tts.infer(text=text_input)
tts.save(audio, "outputs/remote_output.wav")
print("💾 Saved remote synthesis to: outputs/remote_output.wav")

# Zero-shot voice cloning (encodes audio locally, sends codes to server)
if os.path.exists("examples/audio_ref/example_ngoc_huyen.wav"):
    cloned_audio = tts.infer(
        text="Đây là giọng nói được clone và xử lý thông qua phuonganh-tts Server.",
        ref_audio="examples/audio_ref/example_ngoc_huyen.wav",
        ref_text="Tác phẩm dự thi bảo đảm tính khoa học, tính đảng, tính chiến đấu, tính định hướng."
    )
    tts.save(cloned_audio, "outputs/remote_cloned_output.wav")
    print("💾 Saved remote cloned voice to: outputs/remote_cloned_output.wav")
```
*For full implementation details, see: [examples/main_remote.py](examples/main_remote.py)*

### Voice Preset Specification (v1.0)
phuonganh-tts uses the official `phuonganh-tts.voice.presets` specification to define reusable voice assets. Only `voices.json` files following this spec are guaranteed to be compatible with phuonganh-tts SDK ≥ v1.x.

### 3. Advanced Configuration

Customize the server to run specific versions or your own fine-tuned models.

**Run the 0.3B Model (Faster):**
```bash
docker run --gpus all ghcr.io/mvu696841111/phuonganh-tts:serve --model Nemmer/phuonganh-tts-v2 --tunnel
```

**Serve a Local Fine-tuned Model:**
If you have merged a LoRA adapter, mount your output directory to the container:
```bash
# Linux / macOS
docker run --gpus all \
  -v $(pwd)/finetune/output:/workspace/models \
  ghcr.io/mvu696841111/phuonganh-tts:serve \
  --model /workspace/models/merged_model --tunnel
```

---

## 🔬 4. Model Overview <a name="backbones"></a>

| Model | Format | Device | Bilingual | Features | Speed |
|---|---|---|---|---|---|
| **phuonganh-tts-v2** | PyTorch | **GPU** | ✅ | **Podcast, En-Vi CS** | **Fast (LMDeploy)** |
| **phuonganh-tts-v2-CPU** | GGUF/ONNX | **CPU/Edge** | ✅ | **Podcast, En-Vi CS** | **Extreme Speed** |
| **phuonganh-tts-v2-Turbo** | GGUF/ONNX | **CPU/Edge** | ✅ | Lightweight En-Vi | **Ultra Fast** |
| **phuonganh-tts (v1)** | PyTorch | GPU/CPU | ❌ | Stable (Vi only) | Standard |

> [!TIP]
> Use **Turbo v2** for AI assistants, chatbots, and real-time edge applications where speed is critical. Note: It may have stability issues with very short phrases (< 5 words).
> Use **GPU/Standard** (phuonganh-tts v1/v2) for maximum audio quality and high-fidelity voice cloning.

---

## 🚀 5. Roadmap <a name="roadmap"></a>

- [x] **phuonganh-tts-v2**: Full high-fidelity bilingual architecture with **Podcast Mode** and **Voice Cloning**.
- [x] **phuonganh-tts-Codec**: Optimized neural codec for Vietnamese (ONNX).
- [x] **Turbo Voice Cloning**: Bringing instant cloning to the lightweight Turbo engine.
- [ ] **Mobile SDK**: Official support for Android/iOS deployment.

---

## 🤝 6. Support & Contact <a name="support"></a>

- **Hugging Face:** [Nemmer](https://huggingface.co/Nemmer)
- **Discord:** [Join our community](https://discord.gg/yJt8kzjzWZ)
- **License:** Apache 2.0 (Free to use).

---
## 📑 7. Citation <a name="citation"></a>

```bibtex
@misc{phuonganh-ttstts2026,
  title        = {phuonganh-tts-v2: Advanced Vietnamese Text-to-Speech with Podcast and Code-Switching Support},
  author       = {PhuongAnh-TTS Contributors},
  year         = {2026},
  publisher    = {Hugging Face},
  howpublished = {\url{https://huggingface.co/Nemmer/phuonganh-tts-v2}}
}
```

---

## 🌟 Star History

[![Star History Chart](https://api.star-history.com/svg?repos=mvu696841111/PhuongAnh-TTS&type=Date)](https://star-history.com/#mvu696841111/PhuongAnh-TTS&Date)

---

## 🤝 Contributors

Thanks to all the amazing people who have contributed to this project!

<a href="https://github.com/mvu696841111/PhuongAnh-TTS/graphs/contributors">
  <img src="https://contrib.rocks/image?repo=mvu696841111/PhuongAnh-TTS" />
</a>

---

## 🙏 Acknowledgements

This project uses [neucodec](https://huggingface.co/neuphonic/neucodec) for audio decoding.

**Made with ❤️ for the Vietnamese TTS community**
# PhuongAnh-TTS
