# Gemma 4 Chat Template (llama.cpp / OpenWebUI)

Custom Gemma 4 chat template designed for use with **llama.cpp** and **OpenWebUI**.

## Overview

This template is based on the newer official Gemma 4 format but modified to fix an issue where reasoning-channel tokens (e.g. `thought`, `<|channel>`) were leaking into visible outputs.

The goal is to:
- ✅ Keep modern tool-calling behavior
- ✅ Maintain compatibility with llama.cpp
- ❌ Prevent thinking-channel leakage in responses

## Changes from Official Template

- Removed replay of:
  - `message.reasoning`
  - `message.reasoning_content`
- Removed forced empty:
  - `<|channel>thought ... <channel|>`
- Kept:
  - Tool-call handling
  - Tool-response formatting
  - Assistant continuation logic

## Why This Exists

The official Gemma 4 template assumes a serving stack that properly handles reasoning channels.

In some setups (like llama.cpp + OpenWebUI), these markers may appear in the final output. This template removes those problematic parts while keeping everything else intact.

## Usage

Replace your current chat template with the modified version.

Works with:
- llama.cpp (peg-gemma4)
- OpenWebUI

## Notes

You may still see this warning in llama.cpp:
