# Mały model w przeglądarce / A small model in the browser

Qwen3.5 0.8B running 100% locally in the browser (WebGPU, ONNX, Transformers.js 4.3.1).
An educational playground: the same question, different generation settings, different answer.

Live: https://workszop.github.io/qwen/

## What you can control

| Parameter | Acts on | Notes |
|---|---|---|
| System prompt | input | role, language, style |
| Conversation memory | input | off = every message is a fresh start |
| Thinking mode | chat template | `enable_thinking` flag, reasoning shown in a collapsible block |
| Greedy vs sampling | token choice | greedy = identical answers every time |
| Temperature | logits | 0.1 to 2.0 |
| Top-k, Top-p | filters | 0 / 1.0 = off |
| Repetition penalty, no-repeat n-gram | logits / filter | watch the language break above 1.5 |
| Max / min new tokens | stopping | min blocks the end token |
| Image | input | multimodal, 448×448 |

A random seed is not available: Transformers.js samples with `Math.random`, so use greedy decoding when you need repeatability.

Nine preset experiments set the parameters and fill in a prompt. The ×3 button sends the same message three times to show the spread. PL / EN, language persisted in `localStorage`.

## Run locally

```bash
python3 -m http.server 8080
```

Open http://localhost:8080/ in Chrome or Edge with WebGPU. First load downloads about 850 MB into the browser cache.

Model: [onnx-community/Qwen3.5-0.8B-ONNX-OPT](https://huggingface.co/onnx-community/Qwen3.5-0.8B-ONNX-OPT) (Apache 2.0). Design: edulab.
