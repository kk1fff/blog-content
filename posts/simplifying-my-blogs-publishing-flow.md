---
title: Simplifying My Blog’s Publishing Flow
description: >-
  Separating draft and published articles from review and deployment, with fixed
  revisions and previews that make updates easier to follow.
tags:
  - agentic-workflow
  - static-sites
  - writing
publishedAt: '2026-10-09T00:00:00.000Z'
draft: false
---
In [The Local Loop Behind an Agentic Blog](/posts/the-local-loop-behind-an-agentic-blog/), I described how a post moves from a conversation to a local render, through review, and finally to the public site.

As I developed that workflow, the article model became harder to explain than the writing process itself. It mixed whether an article was public with what the agent was doing to publish it.

This update separates those concerns. An article has two statuses: **draft** and **published**. Review and deployment have their own progress.

## Two statuses, two clear meanings

A draft appears in the local workspace preview and stays out of the public site. A published article appears in both.

Staging, waiting for review, publishing, and waiting for a pull request to merge still matter. They describe an operation in progress. Keeping them separate lets me ask two useful questions independently: “Can readers see this article?” and “What needs to happen next?”

An older article whose live revision has not been verified can still be recorded as published, with separate verification metadata. Uncertainty about a deployment does not require another article status.

## Editing keeps the public version available

Suppose I want to revise an article that readers can already access. It stays published while I work. The public site continues serving the existing revision, and the local workspace shows my changes.

The system tracks three versions:

- **Working revision:** the article I am editing.
- **Staged revision:** the fixed candidate prepared for review.
- **Live revision:** the version available to readers.

A `hasPendingChanges` flag identifies work that has not reached the public site.

That distinction also helps when writing and deployment overlap. If I submit one revision and then keep editing, the submitted revision can become live while the newer local changes remain pending. Completing a deployment should only complete the work it actually contains.

## Two previews for different moments

My workspace runs on a remote computer that I access through Tailscale. The Preview MCP starts a browser server there and returns complete clickable addresses, with Tailscale addresses first.

The **workspace preview** includes every local article, including drafts, in navigation, tags, and search. It is where I explore the blog as it currently exists in the workspace. After edits, I reopen it to build an updated view.

The **staged preview** captures a particular article and its assets against the production baseline. It gives review a stable target: the candidate I approve is the candidate prepared for publication.

The preview remains available while the conversation continues, so I can inspect the page and discuss changes with the agent.

## Review belongs to a revision

The publishing sequence now makes that stable target explicit:

1. Create or edit the article and explore the workspace preview.
2. Stage a fixed revision.
3. Inspect that revision at desktop and phone sizes.
4. Review the wording and approve the candidate.
5. Publish it through the Content MCP.
6. Track deployment until the live revision is verified.

Feedback produces another revision, which needs fresh preview checks and approval. Screenshots of the changing workspace cannot stand in for inspecting the fixed publication candidate.

The responsibilities remain small. Content MCP manages staging, approval, and publication. Preview MCP provides browser access and screenshots.

The existing `commit_and_publish` tool handles delivery according to the saved policy: direct push or a pull request. `blog_status` tracks what happens afterward. A successful push is one step toward publication; a pull request also waits for merge. Publication succeeds after deployment and live verification.

## Enough context to resume the work

The agent can find drafts, published articles with pending edits, and unfinished publishing operations through the existing tools. Separate progress records tell it whether to request review, wait for a merge, investigate a failure, or resume publication.

Existing lifecycle records migrate while preserving snapshots, approvals, and publication history. The agent instructions and documentation follow the same model.

## Implementation and rollout

At the time of this update, the refactor is implemented locally. The implementation checks recorded in my notes include a passing build, all 50 tests passing, and desktop and phone preview inspection.

Production rollout remains pending: updating the deployed engine, reconnecting MCP clients, checking Tailscale access from another device, and validating a real GitHub Pages deployment.

The change makes the everyday writing model easier to follow. I can keep improving an article while readers see its current public version, review a fixed candidate with the agent, and track that candidate all the way to the live site.
