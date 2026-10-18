<div align="center">

<img src="./assets/loom-logo.svg" alt="Loom" width="96" height="96" />

# Loom

### Weave a single sentence into an interactive prototype.

**Text to interactive high-fidelity prototype, in one file.**

[![Version](https://img.shields.io/badge/version-1.0.0-6366f1?style=flat-square)](./CHANGELOG.md)
[![Made with HTML](https://img.shields.io/badge/Made%20with-HTML-6366f1?style=flat-square)](.)
[![Zero Build](https://img.shields.io/badge/Build-Zero-22c55e?style=flat-square)](.)
[![Single File](https://img.shields.io/badge/Deploy-Single%20File-6366f1?style=flat-square)](.)
[![No Backend](https://img.shields.io/badge/Backend-None-22c55e?style=flat-square)](.)
[![License](https://img.shields.io/badge/License-MIT-f59e0b?style=flat-square)](./LICENSE)

**English** · [简体中文](./README.md) · [Live Demo](https://leixiangjian.github.io/loom/) · [Issues](https://github.com/your-org/loom/issues)

</div>

---

## Table of Contents

- [What is Loom](#what-is-loom)
- [Core Features](#core-features)
- [Quick Start](#quick-start)
- [Supported Models](#supported-models)
- [Workflow](#workflow)
- [UI Tour](#ui-tour)
- [Architecture](#architecture)
- [Data & Privacy](#data--privacy)
- [FAQ](#faq)
- [Roadmap](#roadmap)
- [Contributing](#contributing)
- [Acknowledgments](#acknowledgments)
- [License](#license)

---

## What is Loom

**Loom** is a **ready-to-use AI-powered high-fidelity UI prototyping platform**.

Feed it a requirement — a sentence, a Markdown file, a Word document, or a PDF PRD — and Loom calls an LLM to **weave** it into a **self-contained, interactive HTML prototype** that runs directly in your browser.

> **Loom** means "weaving machine." It takes scattered threads of requirements and weaves them into one coherent fabric of a prototype.

Unlike traditional prototyping tools, Loom is **a single HTML file**:

- No `npm install`
- No build step
- No backend
- No sign-up

Open it and use it. Export it and run it. **What you get isn't just a generated result — it's a generation tool.**

### Why Loom

AI prototyping tools today fall into two camps:

- **Closed SaaS** (v0, Lovable, Bolt): powerful and polished, but locked to accounts, providers, and their infrastructure.
- **Code generators** (Cursor, Claude Code): flexible, but require a developer environment — PMs and designers can't easily use them.

Loom fills the middle path: **PMs, designers, and indie developers can open a browser and use it, data stays local, and the output is a deliverable single file.**

### Core Principles

| Principle | Implementation |
|-----------|----------------|
| **Single file** | Zero build, zero deployment — one `index.html` is everything |
| **Fully frontend** | No middle server, no telemetry, no data upload |
| **Self-contained output** | Generated prototypes use only inline CSS/JS, run by double-click |
| **Multi-model** | Not tied to any provider — local OpenCode, 8 cloud providers, or custom endpoints |
| **Defensive** | Multi-layer fallbacks on every response, file, and structure, with clear errors |

---

## Core Features

### 📥 Multi-format Requirement Input

| Format | Supported | Implementation |
|--------|:---------:|----------------|
| Plain text | ✅ | Type directly into the left panel |
| Markdown (`.md` / `.markdown`) | ✅ | `FileReader.readAsText` |
| Plain text (`.txt`) | ✅ | `FileReader.readAsText` |
| Word (`.docx`) | ✅ | Native ZIP parsing + `DecompressionStream` + XML extraction |
| PDF (`.pdf`) | ✅ | pdf.js loaded on demand, page-by-page text extraction |

- Drag & drop or click to import
- Preview of the first 800 characters shown automatically
- Auto-switches to the "File" tab to avoid using stale text
- Shows file size and parsed character count

> Legacy `.doc` is not supported — you'll be prompted to save as `.docx`.

### 📱 Three Target Devices

Loom injects the corresponding design guidelines into the system prompt:

| Device | Viewport | Key guidelines |
|--------|----------|----------------|
| 📱 Mobile | 393 × 852 | Single column / bottom tab bar / 44px touch targets / body 14-15px |
| 💻 Web | 1440 × 900 | Sidebar + multi-column / hover states / body 14-16px |
| 🖥️ Tablet | 820 × 1180 | Collapsible sidebar / two-column / stylus-friendly / body 15-16px |

The preview panel **follows the selected target device automatically**.

### 🔌 Multi-model Support

**OpenCode local direct** (recommended, free to use)
- Fetch all models from your local OpenCode server
- Browse and pick from "Free / All"
- Leave blank to use OpenCode's default model
- Supports server password authentication

**Cloud providers** (8 + custom)

| Provider | Default model | Free tier |
|----------|---------------|-----------|
| Anthropic | `claude-opus-4-5-20251101` | Paid |
| OpenAI | `gpt-4o-mini` | Paid |
| Groq | `llama-3.3-70b-versatile` | ✅ 30 RPM / 1K RPD |
| Cerebras | `llama3.3-70b` | ✅ 30 RPM / 14.4K RPD |
| OpenRouter | `llama-3.3-70b-instruct:free` | ✅ 20 RPM / 50 RPD |
| SambaNova | `DeepSeek-V3.1` | ✅ 60 RPM / 12K RPD |
| Gemini | `gemini-2.5-flash` | ✅ Generous |
| Mistral | `mistral-small-latest` | ✅ Phone verification required |
| Custom | Manual input | Depends on endpoint |

**Centralized config**: provider, endpoint, key, and model all live in the "Model Config Center" modal — no clutter in the workspace.

### 🎨 Controllable Generation

**Skills** (injected into the system prompt as constraints)
- High-fidelity / Design system / Anti-AI-slop / Interaction / Responsive / Dataviz

**Design directions** (influence visual style)
- Minimal business / Warm & approachable / Dark tech / High-contrast data / Editorial / Soft Morandi

**Generation trace** (timeline)
- Shows each step: prepare session → send request → response returned → parsed
- Green = success, red = error, blue = info
- Collapsible panel, quick to locate failures

### 💬 Iterative Refinement

No restart from scratch.

- Describe changes in the right panel ("buttons are too small", "add a confirmation dialog", "switch to dark theme")
- Loom packages **current HTML + feedback** into an incremental prompt
- The new version replaces the preview; the old version isn't kept (iteration count visible in trace)

> Iterations reuse the same OpenCode session to preserve context; the first generation creates a new session.

### 🔍 Live Streaming Preview

As the LLM streams, Loom renders:

- Throttled preview updates every 500ms
- Skeleton first, content fills in
- File size displayed live in the chat panel

### 🖥 Fullscreen Focus

- Click the fullscreen button, or press `F`
- Toolbar stays visible — switch devices, refresh, or exit anytime
- Trace panel hides automatically in fullscreen for focus

### 📤 Three Export Formats

| Format | Implementation | Best for |
|--------|----------------|----------|
| **HTML** | Direct download as self-contained file | Double-click, embed, share with clients |
| **Word** | Wrapped as `.doc` with mso headers | Delivering as design documentation |
| **PDF** | Hidden iframe triggers browser print | PDF archiving or print review |

> Exported HTML has no external dependencies and can be deployed directly to GitHub Pages / Vercel / Nginx.

### 🛡 Security & Isolation

- Generated HTML runs in a `sandbox="allow-scripts"` iframe
- Preview cannot access parent DOM, cookies, or localStorage
- Generated HTML is constrained to be fully self-contained (no CDN, external fonts, or external images)

---

## Quick Start

### Requirements

- A modern browser (Chrome / Edge / Safari / Firefox)
- No Node.js, no backend needed
- Internet access for PDF import (pdf.js loaded on demand)

### Three Steps

**① Get Loom**

```bash
git clone https://github.com/your-org/loom.git
cd loom