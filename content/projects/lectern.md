---
title: "Lectern"
date: 2026-11-15
description: "A local-first desktop app that turns open courses into study courses you own."
summary: "A Tauri + Rust desktop app that turns YouTube playlists, MIT OCW, NPTEL, OpenStax, LibreTexts and Open Yale into structured courses with offline video, timestamped notes, progress tracking and spaced repetition. All data stays on your machine."
github: "https://github.com/devvspaces/oplearn"
tags: ["Rust", "Tauri", "SQLite", "React", "TypeScript"]
features:
  - title: "Courses from open sources"
    description: "Imports YouTube playlists (Data API or yt-dlp), MIT OCW, NPTEL, OpenStax, LibreTexts and Open Yale into modules and lessons, keeping each license and source link."
  - title: "Offline study player"
    description: "A download queue with resume and verification, a local Range-serving media server, and the YouTube player behind our own controls and hotkeys."
  - title: "Notes, search and review"
    description: "Notes anchored to a video time or a PDF page, SQLite FTS5 search across transcripts, notes and PDFs, and SM-2 flashcards."
code: |
  pub fn review(s: CardState, grade: Grade) -> CardState {
      let q = f64::from(grade.quality());
      let ease = (s.ease + (0.1 - (5.0 - q) * (0.08 + (5.0 - q) * 0.02)))
          .max(MIN_EASE);
      if grade.quality() < 3 {
          return CardState { ease, interval_days: 1, repetitions: 0 };
      }
      // ...1 day, 6 days, then interval × ease
  }
---

Lectern turns long-form lectures and open textbooks into courses you can actually study: offline, structured, and tracked.

### Architecture

- **Rust owns all state.** A Tauri v2 core with SQLite (hand-rolled migrations, FTS5 search). The React 19 renderer talks to it through typed commands generated with tauri-specta.
- **Imports.** Each provider (MIT OCW, NPTEL, OpenStax, LibreTexts, Open Yale) builds a pure import plan that is written to the database in one step and rolled back if anything fails. Requests are rate-limited per provider and catalogues are cached for 24 h.
- **Downloads.** yt-dlp and ffmpeg run as verified sidecars. A queue with live concurrency, pause and resume through `.part` files, and ffprobe checks before a file counts as downloaded.
- **Playback.** A loopback HTTP server serves media with Range support and hosts the YouTube IFrame bridge, which avoids embed error 153 inside a webview.
- **Progress.** Watch time is merged into intervals to auto-complete lessons, with study plans, streaks and reminders on top.
- **Optional AI.** You bring your own Anthropic key. Each request shows a cost estimate first, stays within a monthly budget, and cites anchors back to transcript times and PDF pages.

### Key Features

- **Courses from open sources**, with licenses and source links kept.
- **Timestamped notes**, bookmarks, questions and to-dos, plus notes anchored to PDF pages.
- **Spaced repetition** (SM-2), quizzes and ⌘K search across everything.
- **Backups:** daily SQLite snapshots, restore, and a full JSON export.

No telemetry. API keys live only in the OS keychain.
