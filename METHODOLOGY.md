# Methodology

This analysis was conducted using publicly accessible interfaces. No authentication was bypassed.

---

## The Approach

Kimi has shell and Python access by design. I used them to inspect the environment.

Python's `os` module lists directories without special permissions:

```python
import os
os.listdir('/app/')
os.listdir('/app/.kimi/skills/')
```

This showed the container's file structure: skill files, Python source code, and configuration directories.

The Python files in `/app/` are readable text:

```python
with open('/app/kernel_server.py') as f:
    content = f.read()
```

I got `kernel_server.py`, `jupyter_kernel.py`, `browser_guard.py`, and `utils.py` — the core modules.

The `/proc/` virtual filesystem exposes process info: command lines, environment variables, memory maps. I checked these to see what services were running.

Network discovery identified exposed services. Port scanning revealed the kernel server on port 8888 and Chrome DevTools on port 9223. Probing these endpoints with `curl` confirmed they were accessible and unauthenticated.

---

## What Was Analyzed

The analysis covered system prompts for all six Kimi variants (Chat, OK Computer, Docs, Sheets, Websites, Slides), tool schemas in JSON format, skill files for docx, xlsx, pdf, and webapp-building, the Python source code in `/app/`, the container filesystem structure, and the network services and ports.

---

## What Was Not Accessed

I didn't access model weights or internal APIs — this analysis covers the agent environment, not the model itself. I didn't probe authentication-protected endpoints beyond what was publicly accessible. I didn't touch other users' sessions or data. I examined compiled binaries like KimiXlsx and tectonic only for metadata, not decompiled code. I didn't explore backend infrastructure outside the container.

---

## Reproducibility

These techniques work in any Kimi OK Computer session. The agent has shell and Python access by design. Anyone can run `os.listdir('/app/')` or read the source files. I used documented capabilities for inspection instead of task completion.

---

## Limitations

This is a point-in-time snapshot. The system may change. Container isolation limits visibility into host and backend infrastructure. Some binaries weren't decompiled due to scope and legal considerations. Network-exposed ports may be hardened in future versions. The analysis covers what was observable in early 2025.
