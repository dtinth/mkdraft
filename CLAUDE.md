# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

`mkdraft` is a simple Ruby utility for managing timestamped markdown drafts. It reserves the next available filename for a new draft based on the current date and maintains state about the latest draft number.

## Architecture

The entire project is a single executable Ruby script (`mkdraft`) that:

1. Creates a `drafts.local/` directory to store drafts and state
2. Generates timestamped filenames in the format `YYYY-MM-DD_NNN.md` where NNN is a zero-padded incrementing number
3. Persists state in `drafts.local/state.json` to track the latest draft number for the current day
4. Searches for the next available draft number to avoid overwriting files

The script is designed to be run directly as a command and outputs the reserved filename to stdout.

## Common Commands

**Run the script:**
```bash
./mkdraft
```

**Run with Ruby explicitly:**
```bash
ruby mkdraft
```

## Key Implementation Details

- **State Management**: Draft numbering state is stored in JSON format at `drafts.local/state.json`
- **Date Format**: Uses `YYYY-MM-DD` prefix (generated with `Time.now.strftime("%Y-%m-%d")`)
- **Filename Format**: `YYYY-MM-DD_NNN.md` where NNN increments daily (resets when date changes)
- **File Existence Check**: Searches for the next available number to handle edge cases where files are deleted
- **Directory Creation**: Ensures `drafts.local/` exists before writing state
