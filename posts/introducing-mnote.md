---
title: 'Introducing mnote: notes that begin with a folder'
description: >-
  A local-first Markdown notes app for a personal vault—or a small, self-hosted
  group.
tags:
  - mnote
  - notes
  - markdown
  - self-hosting
publishedAt: '2026-09-16T06:21:39.205Z'
updatedAt: '2026-09-16T06:22:09.204Z'
draft: false
---
Most note apps begin by asking you to trust a service. mnote begins with a folder.

mnote is a personal Markdown notes app for a small, local group. Your notes live as ordinary files in a private vault; the app supplies the useful parts around them without making the vault disappear behind a proprietary format.

## A calmer place to keep notes

The daily note is the inbox. From there, pages can grow naturally: freeform Markdown, `[[wiki-links]]`, folders, tags, images, and source or preview views. The point is to make it easy to capture a thought now and decide what it belongs to later.

For the smaller things that should not interrupt a note, mnote has **Park a thought**: capture it quickly, keep the time and context with it, then promote it to a note when it earns one.

## Markdown that stays yours

mnote keeps its durable data in a simple vault:

```
vault/
  notes/
  history/
  parked/
  context/
  assets/
```

That means the notes remain readable on disk and easy to back up. It also means history is tangible: mnote saves note snapshots and lets you inspect or restore a previous revision.

Tags are written in the notes, not trapped in a separate taxonomy. When needed, structured tag search can narrow a result by its surrounding heading or list scope—for example, finding `#grocery` only inside `#shopping`.

## Local first, with room to grow

For one computer, the desktop app opens a folder and works there—no account, password, server, or always-on service required. Its index and preferences live outside the vault, which keeps cloud-synced folders from being churned by app metadata.

When a few people need their own private vaults, mnote can also run as a small self-hosted service. It has a Rust backend, a Vue interface, browser access, and an Electron remote client. A home-hosted instance over Tailscale is the intended shape: your devices can reach it, while the notes remain on your own machine rather than on the public internet.

## Details that make writing less fussy

A few small interactions are especially close to the spirit of the project:

- Type `@` to insert a date from a calendar.
- Edit Markdown tables in a grid, then write them back as normal Markdown pipes.
- Command- or Control-click task boxes directly in source.
- Use the note picker to find or create pages without leaving the keyboard.
- Move between source and preview when each is the more helpful view.

mnote is not trying to turn personal notes into another feed, database, or cloud dependency. It is a quiet workspace for keeping thoughts in files you control—useful alone, and still straightforward when shared with a few trusted people.
