# ArchNemix Pipeline Maintenance

Scheduled maintenance tasks for the [ArchNemix](https://github.com/YTShortMakerArchx) YouTube Shorts generation pipeline.

## What is this repo?

ArchNemix is a self-hosted AI pipeline that generates Reddit-style YouTube Shorts from user-provided text scripts. The pipeline runs across several HuggingFace Spaces:

- **TTS** — Kokoro-82M text-to-speech
- **Aligner** — Montreal Forced Aligner + Qwen3 forced aligner
- **Video** — FFmpeg subtitle burn + encode
- **Controller** — orchestrates all stages, stores intermediate files in a HuggingFace dataset

## Why does this repo exist?

Each pipeline run produces temporary files stored in a HuggingFace dataset:

```
{pipeline_id}/
  audio.wav              # TTS output
  tts_timestamps.json    # word timestamps from TTS
  align_timestamps.json  # word timestamps from forced alignment
  video.mp4              # final rendered short
  meta.json              # creation timestamp for cleanup
```

These files are temporary. Once the user has downloaded their video, the files serve no purpose. This repo contains a scheduled GitHub Actions workflow that runs every 6 hours and deletes any pipeline folder older than 24 hours.

## Workflows

### `cleanup-pipelines.yml`

- **Schedule:** every 6 hour
- **What it does:** reads `meta.json` from each pipeline folder in the HuggingFace dataset, checks the `created_at` timestamp, and deletes the entire folder if it is older than 24 hours
- **Trigger:** also runnable manually from the Actions tab

## Secrets required

Set these in **Settings → Secrets and variables → Actions**:

| Secret | Value |
|--------|-------|
| `HF_TOKEN` | HuggingFace write token with access to the pipeline dataset |
| `HF_DATASET` | Dataset repo ID, e.g. `YTShortMakerArchx/archnemix-pipelines` |

## License

PROPRIETARY SOFTWARE LICENSE — see `LICENSE.txt`
