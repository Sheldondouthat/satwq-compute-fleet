# satwq-compute-fleet

Overflow compute for the SATWQ estate. When the home VM (8 GB) is saturated,
heavy simulation batches run here on GitHub-hosted runners instead of wedging
the box.

**Free-tier facts (verified 2026-10-02):** public repos get unlimited Actions
minutes, 20 concurrent jobs, 6-hour max per job, Linux runners at 1x.

## Dispatch a job

```bash
gh workflow run fleet-job.yml \
  -R Sheldondouthat/satwq-compute-fleet \
  -f command='python3 sim.py --n 1000000 > out/results.json'
```

Or use the local dispatcher (waits for completion, downloads the artifact):

```bash
~/workspace/bin/fleet-run.sh -- python3 sim.py --n 1000000
```

Anything the command writes under `./out/` comes back as a downloadable
artifact (7-day retention). One rule: keep it CPU-bound numerics — no
credentials, no secrets, no private data in dispatched commands.
