# 🎬 AI-Based Real Estate Video Generation System

## 📌 Overview
This project demonstrates an end-to-end pipeline that converts real estate images into short cinematic videos using AI.

The system follows a modular architecture:
- Image → Caption (BLIP-2)
- Caption → Cinematic Prompt (LLM)
- Prompt → Video (Diffusion Model)
- Frames → Final Video (FFmpeg/ImageIO)

---

## 🧠 Pipeline Architecture

```
Images
   ↓
BLIP-2 (Scene Captioning)
   ↓
LLM (Prompt Generation)
   ↓
Video Diffusion Model
   ↓
Frames → Video (.mp4)
```

---

## 🚀 Features

- Automated prompt generation (no manual editing)
- Supports multiple camera movements:
  - Orbital
  - Dolly + Pan
  - Truck
  - Zoom
  - Tilt
- Generates 5-second videos
- Maintains architectural consistency
- Modular and extendable pipeline

---

## ⚙️ Installation

```bash
pip install transformers diffusers accelerate imageio pillow
```

---

## ▶️ Usage

### 1. Generate Captions
Use BLIP-2 to generate captions from images.

### 2. Generate Prompts
Use LLM (Mistral/Qwen) to convert captions into cinematic prompts.

### 3. Generate Video Frames
```python
frames = pipe(
    prompt=prompt,
    num_frames=16
).frames[0]
```

### 4. Save Video
```python
import imageio

imageio.mimsave("output.mp4", frames, fps=3)
```

---

## 🎥 How to Control FPS and Video Length

### 🔹 FPS (Frames Per Second)

FPS controls how fast frames are played.

```python
imageio.mimsave("output.mp4", frames, fps=3)
```

- Increase FPS → smoother motion
- Example:
```python
fps=6
```

---

### 🔹 Video Length

Video length depends on:

```
video_length = num_frames / fps
```

Example:

```python
num_frames = 16
fps = 3

# 16 / 3 ≈ 5 seconds
```

---

### 🔹 To Increase Video Length

Option 1: Increase frames

```python
frames = pipe(prompt=prompt, num_frames=32).frames[0]
```

Option 2: Reduce FPS

```python
fps = 2
```

---

### 🔹 Example (Longer Video)

```python
frames = pipe(prompt=prompt, num_frames=32).frames[0]

imageio.mimsave("output.mp4", frames, fps=4)
```

```
32 / 4 = 8 seconds video
```

---

## ⚠️ Limitations

- Motion may appear GIF-like due to model constraints
- Camera movements are approximated, not physically simulated
- Quality depends on model and compute resources

---

## 🔮 Future Improvements

- Use advanced models (Veo, Kling, Sora-like architectures)
- Add frame interpolation for smoother motion
- Use higher resolution diffusion models
- Add camera motion simulation post-processing

---

## 🙌 Acknowledgements

- Hugging Face Transformers & Diffusers
- Open-source vision-language and diffusion models

---

