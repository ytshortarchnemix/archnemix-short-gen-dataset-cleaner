# ArchNemix Pipeline Maintenance

Scheduled maintenance tasks for the ArchNemix YTShort pipeline — automated cleanup of temporary dataset files.

## What is this repo?

**Archnemix** is a brand. **YTShort** is a tool developed and owned under the Archnemix brand.

YTShort is a self-hosted AI pipeline that generates Reddit-style YouTube Shorts from user-provided text scripts. Temporary files are produced during the pipeline run and need periodic cleanup.

## Why does this repo exist?

This repository contains a scheduled GitHub Actions workflow that automatically deletes temporary pipeline files after a set period. This keeps the pipeline dataset clean and ensures storage is managed efficiently.

## Workflows

### `cleanup-pipelines.yml`

- **Schedule:** runs periodically to clean old pipeline files  
- **Trigger:** can also be run manually from the Actions tab  

> Note: This workflow requires access to HuggingFace datasets via private credentials. Do **not** expose secrets in public repos.

## License

This software is proprietary and all rights are reserved by Archnemix.  
**No part of this code may be used, copied, or distributed without explicit written permission from the owner.**  

See `LICENSE.txt` for full terms.

## Contact

- General: archnemix@gmail.com  
- YTShort tool: ytshort.archnemix@gmail.com
