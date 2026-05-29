# Shrinker - System Architecture & Technical Blueprint

## 1. High-Level Architecture
Shrinker enforces a strict **Clean Architecture** pattern combined with **MVVM**.
*   **UI Layer**: Jetpack Compose, Material Design 3, strictly reacting to `StateFlow` from ViewModels.
*   **Domain Layer**: Pure Kotlin Use Cases containing business rules (e.g., `EstimateCompressionSizeUseCase`, `CalculateBitrateUseCase`).
*   **Data/Processing Layer**: Infrastructure wrappers for File I/O, Media APIs, and local Persistence.

## 2. Technology Stack
*   **Language:** Kotlin
*   **UI Toolkit:** Jetpack Compose
*   **Asynchrony:** Coroutines & Flow
*   **Dependency Injection:** Hilt
*   **Local Database:** Room (for storing "Recent Activity" and analytics)
*   **Background Processing:** WorkManager & Foreground Services

## 3. Core Processing & AI Engines
### 3.1 Edge AI & Semantic Engine (The Moat)
*   **Function Calling SLM**: Integrate `FunctionGemma 270M` (via MediaPipe/TFLite) to map natural language user prompts directly to internal Kotlin function calls (e.g., `compressVideo(resolution=720, targetSizeMB=20)`).
*   **Vision & Embeddings**: Integrate `MediaPipe Tasks API` or custom quantized TFLite models to generate semantic vectors for isolated, in-app workspaces without scanning the broader OS filesystem.
*   **Vector Storage**: Store generated embeddings in an embedded vector database (e.g., ObjectBox or a SQLite Vector extension implementation) to allow ultra-fast similarity searches.
*   **Perceptual Quality Scoring**: Implement a local structural similarity (SSIM) or edge-detection heuristic before enforcing lossy compression limits.
*   **LLM Integration**: Interface with the Android AICore APIs (Gemini Nano) for text summarization of compressed documents.
### 3.1 Advanced Video/Audio Transcoding (`androidx.media3`)
*   **Tooling**: `androidx.media3:media3-transformer`.
*   **Rationale**: Transformer is the modern, scalable successor to raw MediaCodec routing or heavy legacy FFmpeg binaries. It leverages device-specific hardware encoders to drastically reduce transcoding time without bloating the APK size.
*   **Strategy**: Configure video bitrates recursively; adjust scaling, drop frames seamlessly via `TransformationRequest`.

### 3.2 Image Processing
*   **Strategy**: Transition from simple `Bitmap.compress()` to `ImageDecoder` and potentially leveraging native C++ layer tools (via JNI or optimized libraries) if strict EXIF preservation or specific color-space handling is required.
*   **Memory Safety**: Large images will be processed using sampling rates (`inSampleSize`) to avoid `OutOfMemoryError` on constrained devices.

### 3.3 Document (PDF) Processing
*   **Tooling**: Evaluate `PdfBox-Android` or integrating a lightweight Ghostscript port.
*   **Strategy**: Android does not have a native PDF compression API. The blueprint involves parsing PDF objects, extracting image streams, downscaling them via the Image Engine, and re-packing the PDF structure.

## 4. Storage & OS Integration
*   **Storage Access Framework (SAF)**: Use `Intent.ACTION_OPEN_DOCUMENT_TREE` and `ActivityResultContracts.GetContent()` for safe, scoped file access without requiring the broad `MANAGE_EXTERNAL_STORAGE` permission, which triggers aggressive Play Store review audits.
*   **System Intent Filters**: Register `AndroidManifest.xml` intent filters for `android.intent.action.SEND` and `SEND_MULTIPLE` on mime-types like `image/*`, `video/*`, and `application/pdf`.

## 5. Background Task Resilience
For long-running batch compressions (especially Video), the app will delegate processing to a `Foreground Service` tightly coupled with `WorkManager`. This guarantees:
1.  The Android OS doesn't kill the process while the user backgrounds the app.
2.  A persistent system notification shows real-time progress.

## 6. Testing & Quality Assurance
*   **Unit Tests**: JUnit + MockK for Use Cases and size formatting logic.
*   **Integration Tests**: Robolectric for Android-dependent media extraction parsing.
*   **Visual Regression Tests**: Roborazzi for verifying Compose UI consistency during theming changes or scaling on tablets/foldables.
