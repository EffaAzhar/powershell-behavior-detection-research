# Behavioral Detection of Suspicious PowerShell Activity Using Log Analysis

## Project Objective
This project investigates whether suspicious PowerShell activity can be distinguished from benign administrative usage through behavioral log analysis in a controlled Windows virtual machine environment.

## Research Question
Can suspicious PowerShell execution be identified using behavioral indicators extracted from PowerShell operational logs?

## Environment
- Host machine: MacBook Pro
- Virtualization: UTM
- Guest OS: Windows 11 ARM
- Logging source: PowerShell Operational Logs
- Purpose: Build a small research dataset of benign and suspicious PowerShell behavior

## Current Progress
- Installed UTM on macOS
- Created Windows 11 virtual machine
- Configured VM safely without shared folders
- Completed Windows installation
- Opened PowerShell as Administrator
- Enabled Script Block Logging
- Enabled Module Logging
- Verified log generation in Event Viewer
- Began generating benign and suspicious PowerShell activity

## Repository Structure
- `README.md` — project overview
- `docs/setup-log.md` — detailed setup record
- `docs/methodology.md` — research methodology
- `docs/data-generation.md` - generate a controlled dataset
- `logs/` — exported logs
- `scripts/` — Python analysis scripts
- `results/` — graphs and findings
- `paper/` — project report or draft paper

## Status
In progress.

