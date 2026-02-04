# Reference: Technical Documentation & Deep-Dives

This directory contains comprehensive technical analysis organized by topic. Each subdirectory focuses on a specific area of the Kimi system.

## Organization

### [runtime/](runtime/) - Core Services & Execution
Python modules and services that power code execution:
- Browser automation with Playwright and Chrome DevTools Protocol
- Jupyter kernel management
- FastAPI control plane
- Utilities and browser profile management

### [system-architecture/](system-architecture/) - Design & Architecture
High-level architectural documentation:
- Skill system design (text-based instruction vs API tools)
- Cross-system architecture analysis
- Tool dependency graphs

### [infrastructure/](infrastructure/) - Deployment & Storage
Infrastructure, containers, and data persistence:
- Container architecture and layers
- Filesystem structure
- Workspace organization (/mnt/kimi, /mnt/okcomputer)
- Supporting directories and runtime storage
- Binary dependencies

### [security/](security/) - Security & Threat Model
Security documentation:
- Container isolation
- Port exposure and CORS configuration
- Threat model analysis

### [skills-analysis/](skills-analysis/) - Skill Deep-Dives
Detailed analysis of each Kimi skill:
- [docx/](skills-analysis/docx/) - Word document generation
- [pdf/](skills-analysis/pdf/) - PDF processing and generation
- [webapp/](skills-analysis/webapp/) - React web application builder
- [xlsx/](skills-analysis/xlsx/) - Excel spreadsheet generation

## Reading Guide

**Want to understand a specific topic?**
- System runtime → Start with [runtime/jupyter-kernel.md](runtime/jupyter-kernel.md)
- How skills work → Read [system-architecture/skill-system.md](system-architecture/skill-system.md)
- Infrastructure setup → See [infrastructure/container-infrastructure.md](infrastructure/container-infrastructure.md)
- A specific skill → Browse [skills-analysis/](skills-analysis/)

**Want everything about one skill?**
- Go to the relevant subdirectory under [skills-analysis/](skills-analysis/)
- Each skill folder has analysis, workflow, and implementation details

## File Statistics

- **28 total markdown files**
- **Runtime**: 7 files
- **System Architecture**: 3 files
- **Infrastructure**: 6 files
- **Security**: 1 file
- **Skills**: 11 files (across 4 subdirectories)
