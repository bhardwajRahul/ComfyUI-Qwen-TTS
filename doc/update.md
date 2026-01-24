# Update Log

## 2026-01-24

### Added Generation Parameters
- Added `top_p`, `top_k`, `temperature`, and `repetition_penalty` parameters to all TTS nodes
- These parameters allow fine-tuning of speech generation quality and diversity
- Available in: VoiceDesignNode, VoiceCloneNode, CustomVoiceNode, DialogueInferenceNode

**Parameter Details:**
- `top_p` (0.0-1.0, default 0.8): Nucleus sampling probability
- `top_k` (0-100, default 20): Top-k sampling parameter
- `temperature` (0.1-2.0, default 1.0): Sampling temperature (higher = more random)
- `repetition_penalty` (1.0-2.0, default 1.05): Penalty to reduce repeated tokens

### Bug Fixes
- Fixed `check_model_inputs()` TypeError caused by decorator usage in `transformers==4.57.0`
- Removed parentheses from `@check_model_inputs` decorator in `modeling_qwen3_tts_tokenizer_v2.py`

### Assets & Documentation
- Added `example/example.png` - comprehensive node screenshot
- Added `example/example.json` - example workflow
- Added `example/Multi-character dialogue.json` - multi-role dialogue workflow
- Updated README with new nodes: VoiceClonePromptNode and DialogueInferenceNode

### Repository Maintenance
- Deleted `dev` branch (merged to main)
- Version bumped to 1.0.2

---

## 2026-01-23

### Dependency Compatibility & Mac Support
- **Fixed**: Resolved `transformers` version conflicts with `qwen-tts` dependency
- **Improvement**: Now supports local package import without requiring `pip install qwen-tts`
- **New**: Add MPS (Mac Apple Silicon) support for device detection
- **Note**: The official `qwen-tts` package requires `transformers==4.57.3`, which may conflict with other ComfyUI nodes. This version uses bundled local code to avoid dependency issues.

### New Nodes
- **VoiceClonePromptNode**: Extract and reuse voice features from reference audio
  - Enables "once extracted, multiple uses" workflow
  - Improves efficiency for batch generation with same voice
  
- **DialogueInferenceNode**: Multi-role dialogue synthesis
  - Supports complex multi-speaker scenarios
  - Batch processing with configurable chunk size
  - Automatic silence insertion between dialogue lines

### Improvements
- Refactored audio normalization into shared utility
- Applied monkeypatch globally during model loading
- Enhanced error handling for audio input types
