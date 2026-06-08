---
title: 'FAQ'
meta_title: 'FAQ — Multiplatform Kickstarter'
description: "Frequently asked questions about Multiplatform Kickstarter — the AI Kotlin Multiplatform app builder."
---

## Is Multiplatform Kickstarter a SaaS?

No. It is planned as a local-first desktop app. Core generation, preview, code inspection, and ZIP export happen inside your local workspace. No hosted build environment is required.

## Do I need a cloud account?

No cloud account is required. The core workflow — project generation, code inspection, and ZIP export — runs entirely on your machine.

## What platforms can it generate?

The goal is to generate Kotlin Multiplatform projects targeting Android, iOS, Desktop (JVM — macOS, Windows, Linux), and WASM (browser) from one shared codebase.

## Do I need Android Studio or Xcode installed?

You need Android Studio or IntelliJ IDEA to build and run the generated projects. Xcode is needed to build for real iOS devices. The generator itself runs as a standalone desktop app — you can generate and inspect code without either IDE installed.

## Can I inspect and edit the generated code?

Yes. The product is designed around source-code ownership. You can inspect generated files, browse the full file tree, read every screen, ViewModel, repository, and build script — and export the complete project.

## Can I export the project?

Yes. ZIP export is part of the core workflow. You can open the generated project in Android Studio or IntelliJ IDEA and start building immediately.

## Will it publish directly to app stores?

Store publishing workflows are planned, but the initial focus is prompt-to-project generation, local preview, iteration, code inspection, and ZIP export. Git integration and automated publishing will follow in later releases.

## How is payment handled?

Payments and license keys are handled by Lemon Squeezy. After purchase you receive a license key by email. Enter the key inside the desktop app to unlock Pro features.
