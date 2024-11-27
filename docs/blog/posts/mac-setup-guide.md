---
title: A minimal setup guide for Mac
date: 2024-11-27
description: How I'm setting up my Mac for ML Open Source Development
categories:
  - Mac
  - RWKV
authors:
  - ivanleomk
---

# Setting Up My MacBook for ML Development: A Living Guide

This is a living document that I'll be updating over the next few weeks as I continue setting up and optimizing my new MacBook development environment. While I followed most of Eugene Yan's excellent [minimal setup guide](https://eugeneyan.com/writing/mac-setup/), I made some specific choices based on my workflow needs.

## Core Development Setup

I kept things minimal for my general development environment, following most of Eugene's recommendations but focusing on just the essentials:

<!-- more -->
```bash
# Core development tools I use daily
brew install git htop warp uv node bun
```

Why these specific choices? They form the backbone of my development workflow without adding unnecessary complexity.

### Mkdocs Specific

Since I use mkdocs for my blog and for instructor's documentation, I had to configure `Cairo` support for it. To do so, i installed the required deps as they mentioned in the mkdocs documentation.

```bash
brew install cairo freetype libffi libjpeg libpng zlib
```

I then configured some local paths

```bash
export DYLD_FALLBACK_LIBRARY_PATH=/opt/homebrew/lib
```

And that was good enough for me to get my mkdocs builds running locally.

## Local LLM Development with Jan

One significant deviation from Eugene's guide was choosing Jan instead of the Ollama + OpenWebUI combination. Jan has become my go-to tool for playing with local LLMs because:

1. **Unified Interface**: Instead of juggling multiple terminal processes, Jan provides a single, cohesive environment
2. **Easy Setup**: Getting started is as simple as downloading their binary from their website itself
3. **Local-First Approach**: Perfect for developing and testing LLM applications without relying on external services
4. **Resource Management**: Better control over model loading and management compared to running separate services

## Research and Documentation

For research and documentation, I'm excited about a few specific tools:

### Zotero
I'm particularly looking forward to using Zotero for paper reading and annotation. As I'm diving deeper into ML research, having a solid system for managing academic papers is crucial. Zotero's features that really appealed to me:
- Built-in PDF reader with good markup tools
- Seamless iPad sync for reading on the go
- Better organization than my previous Google Drive setup

### Obsidian + Notion
I'm using a combination of both:
- **Obsidian**: Personal knowledge management and note-taking
- **Notion**: Company-wide documentation and collaboration
  
This dual setup lets me maintain detailed personal notes while staying integrated with my team's documentation workflow.

### Wisprflow

This is a new dictation tool that essentially allows me to dictate. And it runs much faster than the existing one I'm using which is SuperWhisper. So I'm quite excited to see how it's going to turn out as I experiment and learn a bit more about the tool. 

## Upcoming Explorations

I'm planning to explore and document my experience with:

- Setting up efficient paper reading workflows in Zotero
- Integrating Jan with my development process
- Optimizing the Obsidian-Notion workflow to avoid duplicate effort

## References

- Eugene Yan's [Minimal MacBook Pro Setup Guide](https://eugeneyan.com/writing/mac-setup/)
- Jan [Documentation](https://jan.ai/docs/)

*Note: This guide will be updated regularly as I refine my setup and discover new tools that enhance my workflow.*