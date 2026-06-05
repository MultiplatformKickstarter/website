---
title: 'FAQ'
meta_title: 'FAQ — Multiplatform Kickstarter'
description: "Frequently asked questions about Multiplatform Kickstarter — the local AI app builder for Kotlin Multiplatform developers."
---

## Is Multiplatform Kickstarter a SaaS?

No. Multiplatform Kickstarter is a desktop app that runs entirely on your machine. Code generation uses your local LLM — no data is sent to any cloud service. A subscription unlocks features inside the app; generation itself stays local.

## Which platforms can it generate?

It generates Kotlin Multiplatform projects targeting Android, iOS, desktop (JVM — macOS, Windows, Linux), and WASM (browser). All targets share the same Compose Multiplatform UI and Kotlin business logic.

## Do I need Android Studio or Xcode installed?

You need Android Studio or IntelliJ IDEA to build and run the generated projects. Xcode is needed to build and deploy to real iOS devices. The generator itself runs as a standalone desktop app — you can generate and inspect code without either IDE installed.

## Which local models are supported?

Any model compatible with the Ollama API is supported out of the box. You can also connect via any OpenAI-compatible local API endpoint (LM Studio, Jan, llama.cpp). We recommend code-focused models like `qwen2.5-coder`, `deepseek-coder-v2`, or `codestral` for best KMP output quality.

## Can I inspect the generated code?

Yes. The workspace includes a full file tree browser and code viewer. You can read every generated file — screens, ViewModels, repositories, build scripts — before exporting. In-app editing is on the roadmap.

## Will it publish directly to app stores?

Not yet. Store publishing is planned for a future release. The current MVP focuses on project generation, code inspection, and ZIP export. Git integration and automated publishing workflows will follow.

## How are subscriptions handled?

Subscriptions and one-time purchases are handled by Lemon Squeezy, our merchant of record. After purchase you receive a license key by email. Enter the key inside the desktop app to unlock Pro features. No server-side validation is performed by this website.

## Can I use my own model?

Yes. Any Ollama-compatible or OpenAI-compatible API endpoint running locally works. Fine-tuned models, quantized GGUF models, and custom endpoints are all supported as long as they speak the correct protocol.
