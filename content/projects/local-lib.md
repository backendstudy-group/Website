---
title: "Local Lib"
date: 2026-11-15
description: "A fast, local-first desktop library and professional reader for PDFs and ebooks."
summary: "A Tauri + Rust desktop app that indexes your PDFs and ebooks where they sit on disk, pulls real metadata and covers, and gives you a reader built for study: annotations, OCR, offline read-aloud, notes, flashcards and full-text search. Everything stays on your machine."
github: "https://github.com/devvspaces/local-lib-on"
codeLang: "rs"
tags: ["Rust", "Tauri", "SQLite", "React", "TypeScript"]
features:
  - title: "Library that indexes in place"
    description: "Watched folders pick up new, moved and deleted files, BLAKE3 content hashes catch duplicates, and metadata comes from embedded data, ISBN/DOI and Crossref, Open Library or Google Books."
  - title: "Reader for real study"
    description: "PDF, EPUB, MOBI, DjVu, DOCX and more, with highlights, ink and shapes, reflow and crop, OCR for scans, and natural offline read-aloud that can export to M4B audiobooks."
  - title: "Notes, search and review"
    description: "A Markdown notebook with back-links to highlights, SQLite FTS5 search across the library, FSRS flashcards, and citations in 2,800+ CSL styles."
code: |
  pub fn hash_file(path: &Path) -> std::io::Result<String> {
      let mut f = std::fs::File::open(path)?;
      let mut hasher = blake3::Hasher::new();
      let mut buf = vec![0u8; 1 << 16];
      loop {
          let n = f.read(&mut buf)?;
          if n == 0 { break; }
          hasher.update(&buf[..n]);
      }
      Ok(hasher.finalize().to_hex().to_string())
  }
---

Local Lib is a desktop library and reader for people who study and research from books and papers. Your files stay where they are; Local Lib indexes them, remembers where you stopped, and gives you the tools to actually work with them.

### Architecture

- **Rust owns the library.** A Tauri 2 core with SQLite (FTS5 for full-text search). The React 19 frontend talks to it over Tauri commands.
- **Indexing.** Folder scans and file watchers hash each file with streaming BLAKE3, so a moved file is matched rather than re-imported and duplicates are detected by content.
- **Rendering.** pdf.js for PDFs, foliate-js for EPUB/MOBI/FB2/CBZ, DjVu.js for DjVu, and DOCX/ODT converted to EPUB in memory.
- **Offline speech and OCR.** Kokoro and Piper voices plus Moonshine/Whisper speech recognition via sherpa-onnx, and Apple Vision or tesseract.js for OCR. All of it runs locally.
- **Sync.** Through a cloud folder, Dropbox/OneDrive/Google Drive or WebDAV, with optional end-to-end encryption (Argon2id + XChaCha20-Poly1305) and last-writer-wins merges per item.

### Key Features

- **Citations:** 2,800+ CSL styles, BibTeX/RIS/CSL-JSON export, and a global cite-while-you-write palette.
- **Browser extension** that saves the paper or book you're viewing, including open-access PDFs.
- **AI assistant (bring your own key):** research mode that cites `[book:page]`, chapter summaries and semantic search.
- **Reading habits:** goals, study plans, streaks and reminders.
- **Integrations:** KOReader progress sync and Readwise export.

Builds for macOS, Windows and Linux are on the [releases page](https://github.com/devvspaces/local-lib-on/releases).
