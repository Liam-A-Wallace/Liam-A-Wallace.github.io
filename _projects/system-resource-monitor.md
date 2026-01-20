---
layout: project
title: "System Resource Monitor"
description: "Terminal-based system monitor in C displaying real-time CPU, memory, and disk usage with logging capabilities"

github_url: https://github.com/Liam-A-Wallace/SystemResources  # Add your actual GitHub URL
---

## Project Overview

I developed an interactive terminal-based system monitor in C that provides real-time tracking of CPU, memory, disk, and network usage. The tool features multiple display modes and keyboard controls for customizable system monitoring.

## Key Features

- **Interactive Controls:** Real-time keyboard input handling for mode switching
- **Dual Display Modes:** Simple mode (basic metrics) and Advanced mode (detailed breakdowns)
- **Comprehensive Monitoring:** CPU, memory, disk, and network interface tracking
- **Dynamic Network Analysis:** Real-time upload/download rate calculations
- **Color-coded Visualization:** Progress bars with usage-based coloring
- **Non-blocking Input:** Uses select() for responsive keyboard handling

## Technical Details

The system now uses a DisplayFlags struct to manage view configurations, allowing users to toggle features dynamically. The network monitoring implementation parses /proc/net/dev to track interface statistics and calculate transfer rates by comparing byte counts between intervals.

The input handling system employs select() for non-blocking keyboard input, enabling real-time control without interrupting the monitoring display. This allows users to switch between simple and advanced modes, toggle specific metrics, or exit cleanly.

Memory management was enhanced with early exit conditions when parsing /proc/meminfo, improving efficiency. The network rate calculation handles counter resets and provides KB/s measurements for both individual interfaces and total traffic.

## Challenges and Solutions

Non-blocking Input: Implementing responsive controls required learning about select() and file descriptor sets to check STDIN without pausing the monitoring loop.

Network Rate Calculation: The initial implementation struggled with counter wrap-around and rate accuracy. The solution involved delta calculations with bounds checking and proper time-based normalization.

Mode Management: Coordinating the simple/advanced mode transitions while preserving user preferences required careful state management in the DisplayFlags structure.

Real-time Updates: Maintaining smooth display updates while processing network statistics and handling input demanded optimized parsing and efficient data structures.

## Learning Outcomes

This project deepened my understanding of Linux system interfaces and real-time application design. Working with /proc/net/dev taught me about network interface statistics and rate calculation techniques. The non-blocking input implementation provided practical experience with I/O multiplexing.

The mode management system demonstrated the importance of clean state separation and user interface design in system tools. The progressive enhancement from a basic monitor to an interactive tool showed how modular design supports feature expansion.

## Conclusion 

The enhanced system monitor represents a significant evolution from the original version, adding interactivity and network monitoring capabilities. The clean C implementation demonstrates practical system programming techniques while providing a useful tool for system administration and performance analysis. The interactive controls and dual-mode display make it adaptable for both quick checks and detailed system investigation.