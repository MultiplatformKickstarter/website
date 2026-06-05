---
title: "How to Generate Compose Multiplatform Apps from Prompts"
description: "A practical guide to generating Compose Multiplatform apps using AI and local LLMs — covering prompting strategies, architecture, and what to look for in generated code."
date: 2025-05-01
tags: ["Compose Multiplatform", "Tutorial"]
emoji: "✨"
weight: 3
---

Compose Multiplatform makes it possible to write shared UI code in Kotlin that runs on Android, iOS, desktop, and browser — but getting from zero to a structured project still requires setting up Gradle, configuring source sets, writing boilerplate ViewModels, and wiring up navigation.

AI generation changes this significantly. With the right tooling, you can describe a screen in natural language and get working Compose Multiplatform code in seconds. This guide walks through how to do it effectively.

## What you need

To generate Compose Multiplatform apps locally you need:

1. **Ollama** — the local model runtime. Install at `ollama.com`
2. **A code-capable model** — `qwen2.5-coder:32b` or `deepseek-coder-v2:16b` are solid choices
3. **Multiplatform Kickstarter** — the desktop app that connects to Ollama and generates full KMP projects

After installing Ollama, pull your chosen model:

```bash
ollama pull qwen2.5-coder:32b
```

Then point Multiplatform Kickstarter at `http://localhost:11434` in its settings.

## Writing effective prompts for KMP generation

The quality of AI-generated Compose Multiplatform code depends heavily on how you write your prompts. Generic prompts produce generic output.

### Be specific about screens and data

Instead of:
> "Create a fitness app"

Write:
> "Create a fitness tracking app with three screens: a home screen showing today's workout summary, a workout list screen with `LazyColumn`, and a workout detail screen. Use `WorkoutViewModel` with `StateFlow<WorkoutState>`. The `Workout` data class should have `id`, `name`, `duration`, and `calories`."

Specific screen names, component types, data model fields, and state management patterns give the model the vocabulary to produce accurate code.

### Specify your architecture

Compose Multiplatform works with multiple architecture patterns. Be explicit:

```
Use MVVM with:
- StateFlow<ScreenState> in the ViewModel
- collectAsStateWithLifecycle() in Composables  
- Repository pattern for data access
- Koin for dependency injection
```

This prevents the model from mixing patterns or inventing its own.

### Mention dependencies explicitly

The KMP ecosystem has specific, well-maintained libraries. Naming them directly gets better results:

```
Use these libraries:
- Navigation: compose-navigation (androidx)
- DI: Koin for Compose Multiplatform
- Networking: Ktor client
- Serialization: kotlinx.serialization
- Coroutines: kotlinx.coroutines
```

## What good generated Compose Multiplatform code looks like

When generation succeeds, the output should follow Compose Multiplatform conventions. Here's what to look for:

### Shared UI in commonMain

All Composables should live in the `commonMain` source set — this is what makes them truly multiplatform:

```kotlin
// composeApp/src/commonMain/kotlin/com/example/HomeScreen.kt
@Composable
fun HomeScreen(
    viewModel: HomeViewModel = koinViewModel()
) {
    val state by viewModel.state.collectAsStateWithLifecycle()

    Scaffold(
        topBar = { TopAppBar(title = { Text("Home") }) }
    ) { padding ->
        LazyColumn(contentPadding = padding) {
            items(state.items) { item ->
                ItemCard(item = item, onClick = { viewModel.onItemClick(item.id) })
            }
        }
    }
}
```

### ViewModels using KMP lifecycle

The KMP-compatible `ViewModel` is from `androidx.lifecycle:lifecycle-viewmodel`:

```kotlin
// shared/src/commonMain/kotlin/com/example/HomeViewModel.kt
class HomeViewModel(
    private val repository: ItemRepository
) : ViewModel() {

    private val _state = MutableStateFlow(HomeState())
    val state: StateFlow<HomeState> = _state.asStateFlow()

    init {
        viewModelScope.launch {
            repository.getItems().collect { items ->
                _state.update { it.copy(items = items) }
            }
        }
    }
}
```

### Platform-specific code with expect/actual

When platform-specific implementations are needed, the generated code should use `expect`/`actual`:

```kotlin
// commonMain
expect fun getPlatformName(): String

// androidMain
actual fun getPlatformName(): String = "Android"

// iosMain
actual fun getPlatformName(): String = "iOS"
```

## Iterating with prompts

One of the most valuable features of prompt-based generation is iteration. After the initial project, you can refine with follow-up prompts:

- "Add a search bar to the list screen that filters by name"
- "Add a bottom navigation bar with Home, Profile, and Settings tabs"
- "Change the color scheme to use a dark theme with purple as the primary color"
- "Add pull-to-refresh to the list screen"

Each iteration should produce a diff of changes rather than regenerating the entire project.

## What to verify in generated code

AI-generated code requires review before use. Key things to check in generated Compose Multiplatform projects:

**Dependencies** — Verify that the generated `build.gradle.kts` uses current, stable library versions. Models can generate outdated version numbers.

**Source set placement** — Code that should be in `commonMain` shouldn't be in `androidMain`, and vice versa. Platform-specific APIs should only appear in their respective source sets.

**State management** — Look for direct `mutableStateOf` in ViewModels (should use `StateFlow` for KMP compatibility) and improper coroutine scope usage.

**Navigation** — Verify that navigation is using the shared navigation component correctly and not calling platform-specific APIs from shared code.

## Exporting and building

Once you're satisfied with the generated project, export it as a ZIP from Multiplatform Kickstarter. The ZIP contains a fully configured Gradle project:

```
my-app/
├── composeApp/           # Shared Compose Multiplatform UI
│   └── src/
│       ├── commonMain/
│       ├── androidMain/
│       └── iosMain/
├── shared/               # Business logic, repositories
│   └── src/commonMain/
├── androidApp/           # Android entry point
├── iosApp/               # iOS entry point (Xcode project)
├── desktopApp/           # Desktop JVM entry point
├── wasmJsApp/            # Browser WASM entry point
└── build.gradle.kts
```

Open the root folder in Android Studio, sync Gradle, and run. For iOS, open `iosApp` in Xcode.

## Summary

Generating Compose Multiplatform apps with AI is practical today, with the right tools and prompting approach:

- Use Ollama with a code-focused model
- Write specific, structured prompts that name screens, data models, and architecture patterns
- Review generated code for source set placement, dependencies, and state management
- Iterate with follow-up prompts rather than starting over

Multiplatform Kickstarter handles the scaffolding, model connection, and project structure so you can focus on describing what you want to build rather than configuring the build system.

[Join early access](/download/) to try it when the first build ships.
