# 🦜 phuonganh-tts-TTS

[![Awesome](https://img.shields.io/badge/Awesome-NLP-green?logo=github)](https://github.com/keon/awesome-nlp)
[![Discord](https://img.shields.io/badge/Discord-Join%20Us-5865F2?logo=discord&logoColor=white)](https://discord.gg/yJt8kzjzWZ)

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1b9PO-lcGZX9pEkEwQmu8MfhSnjxKrALW?usp=sharing)
[![Hugging Face phuonganh-tts-TTS-v2](https://img.shields.io/badge/%F0%9F%A4%97%20Hugging%20Face-v2-blue)](https://huggingface.co/Nemmer/phuonganh-tts-v2)
[![Hugging Face phuonganh-tts-TTS](https://img.shields.io/badge/%F0%9F%A4%97%20Hugging%20Face-v1-orange)](https://huggingface.co/Nemmer/phuonganh-tts-v2)

<img width="1087" height="710" alt="image" src="https://github.com/user-attachments/assets/5534b5db-f30b-4d27-8a35-80f1cf6e5d4d" />

**phuonganh-tts-TTS-v2** là thế hệ tiếp theo của mô hình chuyển đổi văn bản thành giọng nói (TTS) tiếng Việt chạy trên thiết bị, hỗ trợ **10.000+ giờ dữ liệu** huấn luyện song ngữ, **clone giọng nói tức thì**, và chế độ **Podcast/Hội thoại** chuyên dụng.

> [!IMPORTANT]
> **🚀 phuonganh-tts-TTS-v2 đã ra mắt!**
> Kiến trúc song ngữ chất lượng cao (high-fidelity) hiện đã sẵn sàng với:
> - **10.000+ Giờ dữ liệu:** Độ tự nhiên vượt trội trong cả tiếng Anh và tiếng Việt.
> - **Chế độ Podcast & Đối thoại:** Hỗ trợ đa người nói với các sắc thái biểu cảm.
> - **Zero-shot Cloning:** Clone bất kỳ giọng nói nào chỉ trong 3-5 giây trên tất cả các biến thể v2.

## ✨ Tính năng nổi bật
- **Huấn luyện 10.000+ giờ**: Được huấn luyện trên tập dữ liệu Anh-Việt khổng lồ cho ngữ điệu giống hệt con người.
- **Song ngữ (En-Vi) Code-switching**: Chuyển đổi ngôn ngữ mượt mà ngay trong câu.
- **Chế độ Podcast & Hội thoại**: Hỗ trợ đối thoại đa người nói với khả năng tự động nhận diện nhân vật.
- **Clone giọng nói tức thì**: Clone bất kỳ giọng nói nào chỉ với **3-5 giây** âm thanh mẫu.
- **Hiệu suất cực nhanh**: Được tối ưu hóa cho **GPU (LMDeploy)** và **CPU (GGUF/ONNX)**.
- **Sẵn sàng cho sản xuất**: Tạo âm thanh chất lượng cao 24 kHz, hoạt động hoàn toàn offline.

[<img width="600" height="595" alt="phuonganh-tts-TTS Demo" src="https://github.com/user-attachments/assets/021f6671-2d7f-4635-91fb-88b2ab0ddbcd" />](https://github.com/user-attachments/assets/021f6671-2d7f-4635-91fb-88b2ab0ddbcd)

## 📌 Mục lục

1. [🦜 Cài đặt & Giao diện Web](#installation)
2. [📦 Sử dụng Python SDK](#sdk)
3. [🐳 Server Chất lượng cao (Standard Mode)](#docker-remote)
4. [🔬 Tổng quan mô hình](#backbones)
5. [🚀 Lộ trình phát triển](#roadmap)
6. [🤝 Hỗ trợ & Liên hệ](#support)
7. [📑 Trích dẫn](#citation)

---

## 🦜 1. Cài đặt & Giao diện Web <a name="installation"></a>

### Thiết lập với `uv` (Khuyến nghị)
`uv` là cách nhanh nhất để quản lý các phụ thuộc.
```bash
# Windows:
powershell -c "irm https://astral.sh/uv/install.ps1 | iex"

# Linux/macOS:
curl -LsSf https://astral.sh/uv/install.sh | sh
```

1. **Clone Repo:**
   ```bash
   git clone https://github.com/mvu696841111/PhuongAnh-TTS.git
   cd PhuongAnh-TTS
   ```

2. **Cài đặt các phụ thuộc:**
   - **Lựa chọn 1: Tối giản (Turbo/CPU)** - Nhanh & Nhẹ
     > ⚠️ *Lưu ý: Chế độ này chỉ hỗ trợ **phuonganh-tts-TTS-v2-Turbo (CPU)** — chạy được trên mọi máy không cần GPU, nhưng **chất lượng âm thanh thấp hơn** so với Standard phuonganh-tts-TTS (đặc biệt với câu ngắn < 5 từ). Khuyến nghị dùng để thử nghiệm nhanh hoặc triển khai trên thiết bị yếu.*
     ```bash
     uv sync
     ```
   - **Lựa chọn 2: Đầy đủ (GPU/Standard)** - Chất lượng cao & Chế độ Podcast *(Dành cho người dùng GPU)*
     > 💡 *Lưu ý: Yêu cầu GPU NVIDIA hỗ trợ CUDA (phiên bản CUDA >= 12.8) hoặc Apple Silicon MPS. Cần cài đặt [NVIDIA Toolkit](https://developer.nvidia.com/cuda-downloads) để đạt tốc độ tối đa. Kích hoạt toàn bộ backbone **phuonganh-tts-TTS-v2** để đạt chất lượng âm thanh tối đa và clone giọng nói độ trung thực cao.*

     ```bash
     uv sync --group gpu
     ```

3. **Khởi chạy Giao diện Web:**
   ```bash
   uv run phuonganh-tts-web
   ```
   Truy cập giao diện tại `http://127.0.0.1:7860`.

---

## 📦 2. Sử dụng Python SDK (phuonganh-tts) <a name="sdk"></a>

SDK `phuonganh-tts` mặc định sử dụng **chế độ Standard** (phuonganh-tts-TTS-v2 GGUF + ONNX) khi dùng cục bộ, mang lại sự cân bằng hoàn hảo giữa chất lượng âm thanh cao và tốc độ xử lý thời gian thực trên bất kỳ CPU hay GPU nào.

### Bắt đầu nhanh
```bash
# Cài đặt tối giản (Build llama-cpp từ nguồn - có thể mất chút thời gian)
pip install phuonganh-tts

# Tùy chọn: Dành cho người dùng Windows (CPU pre-built)
pip install phuonganh-tts

# Tùy chọn: Dành cho người dùng macOS (ARM64/Apple Silicon - Kích hoạt Metal GPU)
pip install phuonganh-tts --extra-index-url https://abetlen.github.io/llama-cpp-python/whl/metal/
```

```python
from phuonganh_tts import PhuongAnh

# Khởi tạo chế độ Standard (Mặc định - Chất lượng cao nhất)
tts = PhuongAnh(emotion="natural") # emotion="natural" (giọng tự nhiên - mặc định) hoặc "storytelling" (giọng kể chuyện)

# 1. Tổng hợp đơn giản (sử dụng giọng Nữ miền Bắc mặc định 'Trúc Ly')
text = "Chào bạn. Tôi là phuonganh-tts-TTS, tôi có thể giúp bạn đọc sách, làm chatbot thời gian thực, thậm chí clone giọng nói của bạn."
audio = tts.infer(text=text)

# Lưu thành file
tts.save(audio, "output_Trúc Ly.wav")
print("💾 Đã lưu file output_Trúc Ly.wav")

# 2. Sử dụng Giọng mẫu cụ thể (Preset Voice)
voices = tts.list_preset_voices()
for desc, voice_id in voices:
    print(f"Giọng: {desc} (ID: {voice_id})")

my_voice_id = voices[1][1] if len(voices) > 1 else voices[0][1] # Giọng Tuyên
voice_data = tts.get_preset_voice(my_voice_id)

audio_custom = tts.infer(text="Tôi đang nói bằng giọng của Bác sĩ Tuyên.", voice=voice_data)

# 3. Lưu thành file
tts.save(audio_custom, "output_Tuyen.wav")
print("💾 Đã lưu file output_Tuyen.wav")
```

### 🚀 Chế độ Turbo (Song ngữ & Tốc độ cực nhanh)
Sử dụng `mode="turbo"` để đạt tốc độ xử lý nhanh nhất, đặc biệt tối ưu cho việc đọc song ngữ Anh-Việt (code-switching) trong thời gian thực.
> [!WARNING]
> Chế độ Turbo có chất lượng âm thanh thấp hơn các chế độ khác và có thể gặp lỗi (nhiễu hoặc lỗi âm) đối với các câu quá ngắn.


```python
from phuonganh_tts import PhuongAnh

# Khởi tạo chế độ Turbo (v2-Turbo GGUF)
tts = PhuongAnh(mode="turbo")

# Turbo v2 hỗ trợ chuyển đổi Anh-Việt cực kỳ tự nhiên
text = "Hệ thống điện chủ yếu sử dụng alternating current because it is more efficient."
audio = tts.infer(text=text)

tts.save(audio, "turbo_output.wav")
```

### 🦜 Clone giọng nói Zero-shot (SDK) <a name="cloning"></a>
Clone bất kỳ giọng nói nào chỉ với **3-5 giây** âm thanh. 

> [!TIP]
> **Chế độ Turbo** được khuyến nghị cho việc clone giọng vì không yêu cầu văn bản mẫu (`ref_text`), trong khi **chế độ Standard** (mặc định) yêu cầu cung cấp `ref_text` để đạt độ chính xác cao hơn.

```python
from phuonganh_tts import PhuongAnh

# Sử dụng turbo mode để clone giọng dễ dàng (không cần ref_text)
tts = PhuongAnh(mode="turbo")

# 1. Trích xuất đặc trưng giọng nói (3-5 giây khuyến nghị)
my_voice = tts.encode_reference("examples/audio_ref/example.wav")

# 2. Tổng hợp với giọng đã clone
audio = tts.infer(
    text="Đây là giọng nói được clone trực tiếp bằng SDK của phuonganh-tts-TTS.", 
    voice=my_voice
)

tts.save(audio, "cloned_voice.wav")
```

---

## 🐳 3. Server Chất lượng cao (Standard Mode) <a name="docker-remote"></a>

Triển khai phuonganh-tts-TTS dưới dạng API Server hiệu suất cao (được hỗ trợ bởi LMDeploy) chỉ bằng một câu lệnh duy nhất.

### 1. Chạy với Docker (Khuyến nghị)

**Yêu cầu**: Cần cài đặt [NVIDIA Container Toolkit](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/latest/install-guide.html) để hỗ trợ GPU.

**Khởi chạy Server với Đường hầm công khai (Không cần mở cổng modem):**
```bash
docker run --gpus all -p 23333:23333 -v huggingface_cache:/root/.cache/huggingface ghcr.io/mvu696841111/phuonganh-tts:latest --tunnel
```

*   **Mặc định**: Server sẽ tải model `phuonganh-tts-TTS-v2` để đạt chất lượng tối đa.
*   **Tunneling**: Docker image tích hợp sẵn đường hầm `bore`. Kiểm tra container logs để tìm địa chỉ công khai của bạn (VD: `bore.pub:31631`).

### 2. Sử dụng SDK (Chế độ Remote)

Khi server đã chạy, bạn có thể kết nối từ bất kỳ đâu (Colab, Web App, v.v.) mà không cần tải các model nặng cục bộ.

**Cài đặt**:
```bash
pip install "phuonganh-tts[gpu]"
```

**Sử dụng**:
```python
from phuonganh_tts import PhuongAnh
import os

# Cấu hình
REMOTE_API_BASE = 'http://your-server-ip:23333/v1'  # Hoặc URL từ bore tunnel
REMOTE_MODEL_ID = "Nemmer/phuonganh-tts-v2"

# Khởi tạo (Cực kỳ NHẸ - chỉ tải codec nhỏ cục bộ)
# Cảm xúc mặc định là "natural" (tự nhiên) - đặt emotion="storytelling" cho chế độ kể chuyện
tts = PhuongAnh(mode='remote', api_base=REMOTE_API_BASE, model_name=REMOTE_MODEL_ID, emotion="natural")
os.makedirs("outputs", exist_ok=True)

# Liệt kê các giọng mẫu trên server
available_voices = tts.list_preset_voices()
for desc, name in available_voices:
    print(f"   - {desc} (ID: {name})")

# Sử dụng giọng cụ thể (chọn động giọng thứ hai)
if available_voices:
    _, my_voice_id = available_voices[1]
    voice_data = tts.get_preset_voice(my_voice_id)
    audio_spec = tts.infer(text="Chào bạn, tôi đang nói bằng giọng của bác sĩ Tuyên.", voice=voice_data)
    tts.save(audio_spec, f"outputs/remote_{my_voice_id}.wav")
    print(f"💾 Đã lưu kết quả tại: outputs/remote_{my_voice_id}.wav")

# Tổng hợp chuẩn (dùng giọng mặc định)
text_input = "Chế độ remote giúp tích hợp phuonganh-tts vào ứng dụng Web hoặc App cực nhanh mà không cần GPU tại máy khách."
audio = tts.infer(text=text_input)
tts.save(audio, "outputs/remote_output.wav")
print("💾 Đã lưu kết quả remote_output.wav")

# Clone giọng Zero-shot (Mã hóa âm thanh cục bộ, gửi code lên server)
if os.path.exists("examples/audio_ref/example_ngoc_huyen.wav"):
    cloned_audio = tts.infer(
        text="Đây là giọng nói được clone và xử lý thông qua phuonganh-tts Server.",
        ref_audio="examples/audio_ref/example_ngoc_huyen.wav",
        ref_text="Tác phẩm dự thi bảo đảm tính khoa học, tính đảng, tính chiến đấu, tính định hướng."
    )
    tts.save(cloned_audio, "outputs/remote_cloned_output.wav")
    print("💾 Đã lưu kết quả remote_cloned_output.wav")
```
*Chi tiết xem tại: [examples/main_remote.py](examples/main_remote.py)*

### Quy chuẩn Voice Preset (v1.0)
phuonganh-tts-TTS sử dụng quy chuẩn chính thức `phuonganh-tts.voice.presets` để định nghĩa các tài nguyên giọng nói có thể tái sử dụng. Chỉ các tệp `voices.json` tuân theo quy chuẩn này mới đảm bảo tương thích với phuonganh-tts-TTS SDK ≥ v1.x.

### 3. Cấu hình Nâng cao

Tùy chỉnh server để chạy các phiên bản cụ thể hoặc các model đã được fine-tune của riêng bạn.

**Chạy model 0.3B (Nhanh hơn):**
```bash
docker run --gpus all ghcr.io/mvu696841111/phuonganh-tts:serve --model Nemmer/phuonganh-tts-v2 --tunnel
```

**Serve model đã Fine-tuned cục bộ:**
Nếu bạn đã merge LoRA adapter, hãy mount thư mục đầu ra của bạn vào container:
```bash
# Linux / macOS
docker run --gpus all \
  -v $(pwd)/finetune/output:/workspace/models \
  ghcr.io/mvu696841111/phuonganh-tts:serve \
  --model /workspace/models/merged_model --tunnel
```

---

## 🔬 4. Tổng quan mô hình <a name="backbones"></a>

| Model | Định dạng | Thiết bị | Song ngữ | Tính năng | Tốc độ |
|---|---|---|---|---|---|
| **phuonganh-tts-TTS-v2** | PyTorch | **GPU** | ✅ | **Podcast, En-Vi CS** | **Nhanh (LMDeploy)** |
| **phuonganh-tts-v2-CPU** | GGUF/ONNX | **CPU/Edge** | ✅ | **Podcast, En-Vi CS** | **Rất nhanh** |
| **phuonganh-tts-v2-Turbo** | GGUF/ONNX | **CPU/Edge** | ✅ | En-Vi mượt mà | **Cực nhanh** |
| **phuonganh-tts-TTS (v1)** | PyTorch | GPU/CPU | ❌ | Ổn định (Chỉ Tiếng Việt) | Chuẩn |

> [!TIP]
> Sử dụng **Turbo v2** cho trợ lý AI, chatbot và các ứng dụng thời gian thực trên thiết bị yếu. Lưu ý: Có thể gặp vấn đề ổn định với các câu cực ngắn (< 5 từ).
> Sử dụng **GPU/Standard** (phuonganh-tts-TTS v1/v2) để đạt chất lượng âm thanh tối đa và clone giọng độ trung thực cao.

---

## 🚀 5. Lộ trình phát triển <a name="roadmap"></a>

- [x] **phuonganh-tts-TTS-v2**: Kiến trúc song ngữ chất lượng cao đầy đủ với **Chế độ Podcast** và **Clone giọng nói**.
- [x] **phuonganh-tts-Codec**: Neural codec tối ưu cho tiếng Việt (ONNX).
- [x] **Turbo Voice Cloning**: Mang tính năng clone giọng nói tức thì lên engine Turbo siêu nhẹ.
- [ ] **Mobile SDK**: Hỗ trợ chính thức cho việc triển khai trên Android/iOS.

---

## 🤝 6. Hỗ trợ & Liên hệ <a name="support"></a>

- **Hugging Face:** [Nemmer](https://huggingface.co/Nemmer)
- **Discord:** [Tham gia cộng đồng](https://discord.gg/yJt8kzjzWZ)
- **Giấy phép:** Apache 2.0 (Sử dụng tự do).

---
## 📑 7. Trích dẫn <a name="citation"></a>

```bibtex
@misc{phuonganh-ttstts2026,
  title        = {phuonganh-tts-TTS-v2: Advanced Vietnamese Text-to-Speech with Podcast and Code-Switching Support},
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

## 🤝 Người đóng góp

Cảm ơn tất cả những người tuyệt vời đã đóng góp cho dự án này!

<a href="https://github.com/mvu696841111/PhuongAnh-TTS/graphs/contributors">
  <img src="https://contrib.rocks/image?repo=mvu696841111/PhuongAnh-TTS" />
</a>

---

## 🙏 Lời cảm ơn

Dự án này sử dụng [neucodec](https://huggingface.co/neuphonic/neucodec) để giải mã âm thanh.

**Được thực hiện với ❤️ dành cho cộng đồng TTS Việt Nam**
