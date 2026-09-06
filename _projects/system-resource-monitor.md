---
layout: project
title: "System Resource Monitor"
description: "Built a C-based terminal tool that monitors CPU, memory, and disk usage in real time by parsing Linux system files directly, with optional logging functionality for historical analysis."
technologies: ["C", "Linux", "/proc"]
github_url: https://github.com/Liam-A-Wallace/SystemResources
---

## What it does

A full-screen terminal monitor that reads CPU, memory, swap, disk, and network usage straight from Linux system files (`/proc/stat`, `/proc/meminfo`, `/proc/net/dev`) and redraws a live dashboard every second. It runs in an alternate screen buffer, so the terminal is restored exactly as it was on exit.

## How it's built

- **Live dashboard** – a header bar with hostname, uptime, load average, and time, plus colour-coded progress bars drawn with fractional Unicode block glyphs and aligned to a common column.
- **Two modes** – a simple mode for headline metrics and an advanced mode with per-core CPU bars and a detailed memory breakdown.
- **Trend sparklines** – inline rolling graphs for CPU and memory history.
- **Network table** – per-interface rates sorted by activity, with auto-scaling units (KB/s–GB/s) and cumulative transfer totals.
- **Instant input** – `termios` raw mode for single-key controls (no Enter needed), `SIGWINCH` resize handling, and graceful shutdown on `SIGINT`/`SIGTERM`.
- **Adaptive layout** – bar width adapts to the terminal width so nothing wraps on narrow terminals.

## Notable problems solved

- **Counter rollover** – delta calculations with bounds checking and time-based normalisation for accurate network rates.
- **Responsive controls** – `select()` and raw-mode terminal handling for keystrokes without blocking the refresh loop.
- **Clean exit** – alternate-screen buffer and cursor handling keep the terminal tidy when the monitor quits.
