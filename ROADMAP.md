# Shrinker - Development Roadmap

## ✅ Milestone 0: Project Foundation (Completed)
- [x] Initial project scaffolding and package setup.
- [x] Google AdMob integration.
- [x] "Sleek Interface" Material 3 implementation.
- [x] Ephemeral single-image compression engine.

---

## 🏗️ Milestone 1: The Robust Media Engine (v1.0 MVP)
*Goal: Solidify the primary use-cases (photos and basic video) to achieve app store readiness.*
- [ ] **Architecture Upgrade**: Implement Hilt DI and migrate existing UI to rigid MVVM state structures.
- [ ] **Video Implementation**: Integrate `androidx.media3:media3-transformer` for local video downscaling and bitrate manipulation.
- [ ] **Recent Activity History**: Implement Room Database to serialize and persist stats and file paths for the "Files" dashboard tab.
- [ ] **Share Intent Receiver**: Allow users to share images directly from their gallery *into* Shrinker.

---

## 🚀 Milestone 2: Mass Processing & Resilience (v1.5)
*Goal: Cater to power users with large storage cleanup demands.*
- [ ] **Batch Processing**: Overhaul the media picker to support multiple selective inputs.
- [ ] **Foreground Service**: Implement WorkManager + Foreground notifications to allow users to start a 10-video batch compression, close the app, and let it run.
- [ ] **Audio Pipeline**: Support extraction of audio from video formats, and compressing standalone WAV/FLAC to MP3/AAC.
- [ ] **Custom Presets**: Build a "Setup/Settings" UI for users to define custom resolution limits and compression levels.

---

## 👑 Milestone 3: Shrinker Premium & Documents (v2.0)
*Goal: Introduce monetization maturity via convenience upgrades and our hardest technical challenge (PDFs).*
- [ ] **Google Play Billing Integration**: Implement logic for "Shrinker Premium" (removes ads, unlocks custom themes).
- [ ] **Advanced AI Workflows**: Unlock multi-step FunctionGemma capabilities for Premium users (e.g., transcode + extract chains).
- [ ] **Document Engine**: Integrate PDF stream parsing to identify and shrink embedded rasters.
- [ ] **Share Sheet Forwarding**: Implement the "Shrink -> Share" chained flow, allowing the user to seamlessly share heavy files directly to email via Shrinker.

---

## 🔮 Milestone 4: The Semantic AI Moat (v3.0+)
*Goal: Evolve into a conversational, intelligent workspace using Edge Machine Learning.*
- [ ] **FunctionGemma Integration**: Set up a 270M SLM via MediaPipe to parse natural language inputs into deterministic routing commands (The "Local Command Center").
- [ ] **In-App Semantic Clustering**: Build the UI to visually group active queue items (e.g., "Screenshots", "Presentations") based on on-the-fly local embeddings.
- [ ] **Content-Aware Compression limits**: Integrate saliency detection to protect text and faces during aggressive JPEG/WEBP quantization.
- [ ] **Local LLM Summaries**: Implement Android AICore bindings (Gemini Nano) to summarize PDFs while shrinking them, auto-filling share sheet intents.
