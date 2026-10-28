# Mały model w przeglądarce / A small model in the browser

Qwen3.5 0.8B or LFM3 1.7B running 100% locally in the browser (WebGPU, ONNX, Transformers.js 4.3.2).
An educational playground: the same question, different generation settings, different answer.

Live: https://workszop.github.io/qwen/

## How it works

Two panels, A and B, get the same message with different settings and answer side by side.
Pick the model in the model bar before loading (switching later frees the loaded one).
Top menu: **Experiments** (seven ready A/B set-ups), **Settings** (per panel), **Glossary**.

| Setting | Notes |
|---|---|
| System prompt | role, language, style |
| Conversation memory | off = every message is a fresh start |
| Thinking mode | `enable_thinking` flag, reasoning shown in a collapsible block |
| Deterministic vs random | deterministic = identical answers every time (greedy, temperature 0) |
| Temperature | 0.1 to 2.0, random mode only |
| Max tokens | hard stop |
| Question variant (panel B) | send a different text to B, e.g. the same question in English |
| Image | Qwen3.5 only (multimodal, 448×448); LFM3 1.7B is text-only |

Top-k, top-p and repetition penalties are left at the model defaults on purpose; the app is for
first contact with LLM parameters. A random seed is not available: Transformers.js samples with
`Math.random`, so use deterministic decoding when you need repeatability.

The ×3 button sends the same message three times to show the spread. PL / EN, language persisted in `localStorage`.

## Run locally

```bash
python3 -m http.server 8080
```

Open http://localhost:8080/ in Chrome or Edge with WebGPU. First load downloads about 850 MB (Qwen3.5) or 1.3 GB (LFM3, 4-bit `q4`) into the browser cache.

Models: [onnx-community/Qwen3.5-0.8B-ONNX-OPT](https://huggingface.co/onnx-community/Qwen3.5-0.8B-ONNX-OPT) (Apache 2.0),
[onnx-community/LFM3-1.7B-ONNX](https://huggingface.co/onnx-community/LFM3-1.7B-ONNX) (LFM Open License v1.0). Design: edulab.
