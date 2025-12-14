# **Herculis-CUA-GUI-Actioner-4B-Demo**

> Gradio Demo: Herculis-CUA-GUI-Actioner-4B is a Computer Use Agent (CUA) multimodal model designed for GUI understanding, UI localization, and action execution across web, desktop, and mobile environments. It focuses on visual grounding, intent-driven actioning, and UI-based question answering (VQA), enabling reliable interaction with real-world software interfaces. The model is optimized for efficient inference while maintaining strong accuracy on complex UI workflows.

## Features

- **UI Localization**: Upload screenshots and provide natural language prompts (e.g., "Locate the `microsoft/Fara-7B` model") to predict precise click coordinates in the format `Click(x, y)`.
- **Visual Grounding**: Outputs annotated images with red ellipses marking predicted action points, scaled to the input resolution.
- **Efficient Inference**: Uses bfloat16 precision on CUDA for fast generation (max 128 new tokens); deterministic output with `do_sample=False`.
- **Prompt Engineering**: Structured localization prompts ensure focused responses without extraneous text.
- **Error Handling**: Graceful fallbacks for model loading, resizing, or parsing issues; detailed console logging.
- **Gradio Interface**: Simple UI with image upload, prompt input, and real-time visualization; supports sharing via `share=True`.

## Prerequisites

- Python 3.10 or higher.
- CUDA-compatible GPU (recommended for bfloat16; falls back to CPU but slower).
- Stable internet for initial model download from Hugging Face.

## Installation

### 1. Clone the repository

```
git clone https://github.com/PRITHIVSAKTHIUR/Herculis-CUA-GUI-Actioner-4B-Demo.git
cd Herculis-CUA-GUI-Actioner-4B-Demo
```

### 2. Install dependencies

Create a `requirements.txt` file with the following content, then run:

```
pip install -r requirements.txt
```

**requirements.txt content:**
```
gradio==6.1.0
transformers==4.57.1
numpy
torch
torchvision
accelerate
qwen-vl-utils
requests
pillow
spaces
```

### 3. Run the application

```
python app.py
```

The demo launches at `http://localhost:7860` (or a public URL if using `share=True`).

## Usage

1. **Upload Image**: Provide a UI screenshot (e.g., web page or app interface; pre-loaded example available).

2. **Enter Prompt**: Describe the target element (e.g., "Locate the `microsoft/Fara-7B` model." or "Find the search bar.").

3. **Localize**: Click "Localize" to run inference.

4. **View Results**:
   - Text: Model output with `Click(x, y)` coordinates.
   - Image: Annotated screenshot with a red ellipse at the predicted position.

## Example Output Inference

| Type         | Preview |
|--------------|---------|
| Input Image  | ![Input Image](https://huggingface.co/prithivMLmods/Herculis-CUA-GUI-Actioner-4B/resolve/main/example/example-image.png) |
| Output Image | ![Output Image](https://huggingface.co/prithivMLmods/Herculis-CUA-GUI-Actioner-4B/resolve/main/example/output-image.webp) |

### Example Workflow
- Upload a Hugging Face models page screenshot.
- Prompt: "Locate the `microsoft/Fara-7B` model."
- Output: `Click(450, 300)` and image with red marker on the model card.

## Troubleshooting

- **Model Loading Errors**: Check network; ensure transformers 4.57.1. If flash-attention issues, install via `pip install flash-attn`. Verify CUDA with `torch.cuda.is_available()`.
- **Resizing Fails**: Image processor uses `smart_resize`; input dimensions must be positive. Fallback to original if errors occur.
- **No Coordinates Parsed**: Ensure prompt ends with the target; model outputs deterministic text. Check console for raw response.
- **OOM on GPU**: Reduce batch size or use CPU; clear cache with `torch.cuda.empty_cache()`.
- **Gradio Share Issues**: Run with `debug=True`; public links expire after 72 hours.
- **PIL Warnings**: Update Pillow if resampling errors appear.

## Contributing

Contributions welcome! Fork the repo, create a feature branch, and submit a pull request with tests. Potential enhancements:
- Multi-step action chains.
- Support for type/scroll actions.
- Integration with automation tools like Selenium.

Repository: [https://github.com/PRITHIVSAKTHIUR/Herculis-CUA-GUI-Actioner-4B-Demo.git](https://github.com/PRITHIVSAKTHIUR/Herculis-CUA-GUI-Actioner-4B-Demo.git)

## License

Apache License 2.0. See [LICENSE](LICENSE) for details.

Built by Prithiv Sakthi. Report issues via the repository.
