# Methodology

This analysis was conducted through cleanroom reverse engineering using publicly accessible interfaces. No proprietary code was decompiled, no authentication was bypassed, and no model weights were accessed.

---

## The Approach

Kimi's provided with shell and Python access by design. It used them to inspect the environment after being asked nicely.

Filesystem enumeration was straightforward. Python's `os` module lists directories without special permissions:

```python
import os
os.listdir('/app/')
os.listdir('/app/.kimi/skills/')
```

This revealed the container's file structure, including the skill files, Python source code, and configuration directories.

Source code reading followed naturally. The Python files in `/app/` are readable text:

```python
with open('/app/kernel_server.py') as f:
    content = f.read()
```

This yielded `kernel_server.py`, `jupyter_kernel.py`, `browser_guard.py`, and `utils.py`, which are the core modules that make the agent environment work.

Process introspection provided additional context. The `/proc/` virtual filesystem exposes process information including command lines, environment variables, and memory maps. This helped understand what services were running and how they were configured.

Network discovery identified exposed services. Port scanning revealed the kernel server on port 8888 and Chrome DevTools on port 9223. Probing these endpoints with `curl` confirmed they were accessible and unauthenticated.

---

## What Was Analyzed

The analysis covered system prompts for all six Kimi variants (Chat, OK Computer, Docs, Sheets, Websites, Slides), tool schemas in JSON format, skill files for docx, xlsx, pdf, and webapp-building, the Python source code in `/app/`, the container filesystem structure, and the network services and ports.

---

## What Was Not Accessed

Some things remained out of scope. Model weights and internal model APIs were not accessed: the analysis is purely about the agent environment, not the model itself. Authentication-protected endpoints were not probed beyond what was publicly accessible. Other users' sessions and data were not touched. Compiled binaries like KimiXlsx and tectonic were examined only for metadata, not decompiled. Backend infrastructure outside the container was not explored.

---

## Reproducibility

These techniques work in any Kimi OK Computer session. The agent has shell and Python access by design. Anyone can run `os.listdir('/app/')` or read the source files. This isn't exploiting a vulnerability; rather, it's using documented capabilities for inspection rather than task completion.

---

## Limitations

This is a point-in-time snapshot. The system may change. Container isolation limits visibility into host and backend infrastructure. Some binaries weren't decompiled due to scope and legal considerations. Network-exposed ports may be hardened in future versions. The analysis reflects what was observable in early 2025.
