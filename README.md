
For background and official docs on Whisper and model sizes, see OpenAI’s Whisper page and the GitHub repository. :contentReference[oaicite:0]{index=0}

---

# 5) `.github/workflows/transcribe.yml`

```yaml
name: Transcribe Calls

on:
  push:
    paths:
      - "audio/**"
  workflow_dispatch:

jobs:
  transcribe:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout
        uses: actions/checkout@v4

      - name: Set up Python
        uses: actions/setup-python@v5
        with:
          python-version: "3.11"

      - name: Install FFmpeg
        run: |
          sudo apt-get update
          sudo apt-get install -y ffmpeg

      - name: Install Python deps
        run: |
          python -m pip install --upgrade pip
          pip install -r requirements.txt
          # Optional: install torch for speed (CPU-only wheels still work)
          pip install torch --index-url https://download.pytorch.org/whl/cpu || true

      - name: Transcribe audio
        run: |
          python transcribe.py --model base
        env:
          PYTHONUNBUFFERED: "1"

      - name: Commit transcripts
        uses: stefanzweifel/git-auto-commit-action@v5
        with:
          commit_message: "chore(transcripts): update transcripts"
          file_pattern: transcripts/**
