# Whisper Call Transcriber

Batch-transcribe call recordings in `audio/` and output `.txt`, `.srt`, `.vtt` into `transcripts/`.
Works locally and via GitHub Actions (auto-commits transcripts on push).

## Quick start (local)

1. Install FFmpeg  
   - macOS: `brew install ffmpeg`  
   - Ubuntu: `sudo apt-get update && sudo apt-get install -y ffmpeg`  
   - Windows: install from ffmpeg.org and add to PATH
2. Python deps:
   ```bash
   pip install -r requirements.txt
