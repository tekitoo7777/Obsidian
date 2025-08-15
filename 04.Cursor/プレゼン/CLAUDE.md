# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

This repository contains educational materials and presentations about Cursor and Obsidian, primarily in Japanese. The content focuses on:
- Educational presentations for teaching staff about Cursor
- Integration workflows between Cursor and Obsidian
- Automation systems using Discord, Dify, and n8n

## Structure

The repository is organized as follows:
- `2025.08.08Cursor勉強会/` - Contains presentation materials for a Cursor workshop aimed at educators
  - Marp format presentations (for slideshow presentations)
  - Notion format documentation (for detailed reference)
  - Supporting images and usage guides

## Working with Marp Presentations

When working with Marp markdown files (`*_Marp.md`):

### Converting to PDF
```bash
marp [filename].md --pdf
```

### Converting to HTML
```bash
marp [filename].md --html
```

### Running presentation server
```bash
marp [filename].md --server
```

### Installing Marp CLI (if needed)
```bash
npm install -g @marp-team/marp-cli
```

## Content Guidelines

This repository contains educational content in Japanese. Key themes include:
- Making Cursor accessible to non-programmers, especially educators
- Practical examples of educational applications (submission management, classroom tools)
- Integration between different productivity tools

## Target Audience

The materials are designed for:
- Education professionals (teachers, instructors, educational support staff)
- Cursor beginners
- People with no programming experience

## Presentation Structure

The main workshop presentation follows this structure:
1. Introduction (3 minutes) - Basic information about Cursor
2. Getting Started with Cursor (5 minutes) - Installation and setup
3. Recommended Plugins (3 minutes) - Useful extensions for education
4. Practical Examples (7 minutes) - Real-world educational applications
5. Summary & Next Steps (2 minutes) - Resources and learning paths