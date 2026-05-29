# Shrinker - Product Requirements Document (PRD)

## 1. Executive Summary & Value Proposition
**Shrinker** is a premier, local-first utility designed to reclaim device storage and optimize media for sharing. In an era of 4K/8K video and high-resolution computational photography, users quickly exhaust their device storage and face bandwidth limits when sharing files. Shrinker solves this gracefully without compromising privacy—performing all compression aggressively and securely on-device with zero cloud dependencies.

## 2. Target Audience
*   **Storage-Constrained Users**: Users holding onto gigabytes of old photos and videos who cannot or will not pay for expanding cloud storage subscriptions.
*   **Professionals on the Go**: Users needing to compress large PDFs, presentation assets, or video clips to bypass email attachment limits.
*   **Privacy Advocates**: Users who require media compression but refuse to upload sensitive corporate or personal documents to web-based "free PDF/Image compressors".

## 3. Core Capabilities
### 3.1 Media Engine
*   **Images**: Smart compression for JPEG/PNG/WEBP. Support for bulk resizing, EXIF metadata stripping (optional for privacy), and format conversion (e.g., HEIC to JPG).
*   **Video**: Resolution downscaling (e.g., 4K to 1080p), framerate capping, and aggressive bitrate reduction using hardware-accelerated HEVC/AVC encoders.
*   **Audio**: Waveform and container conversion (WAV/FLAC to AAC/MP3) with bitrate toggles for voice memos versus music quality.
*   **Documents**: PDF asset down-sampling—locating embedded high-res images within PDFs and reducing their DPI.

### 3.3 The On-Device AI Moat
*   **Natural Language Copilot (FunctionGemma 270M)**: Leverages lightweight, function-calling SLMs allowing users to command the app conversationally. Users can prompt: "Compress these 5 videos to 720p and extract the audio," translating unstructured text into deterministic, local API execution.
*   **In-App Semantic Search & Clustering**: Generates image embeddings strictly for user-selected media within the app's isolated workspace. Allows users to semantically search their active queue or cluster similar files (e.g., "group all whiteboard photos for aggressive compression").
*   **Content-Aware Compression**: Saliency detection algorithms analyze image content to dynamically adjust compression. Preserves crisp edges on text/faces while heavily compressing out-of-focus backgrounds.
*   **Smart Document Summaries**: Leverages Android AICore (Gemini Nano) to generate and attach executive summaries when downscaling massive PDFs or presentation decks.
*   **Batch Operations**: Select multiple files or entire folders to compress overnight.
*   **Share Sheet Integration**: "Shrink & Share" — Intercept outgoing files directly from the Android Share Sheet, compress them on the fly, and forward them to the target app (e.g., WhatsApp, Gmail).
*   **Before & After Previews**: Visual sliders comparing the original vs. compressed image artifacts.
*   **Custom Presets**: Create and save compression profiles (e.g., "Email Ready: 720p Video, Max 20MB", "Archive: High Quality, HEVC").

## 4. Monetization Strategy (Ad-Supported + Convenience Upgrade)
*   **The Zero-Marginal Cost Advantage**: All core processing, batching, and Semantic AI filtering is 100% FREE. Because all compute occurs on-device, we incur no server costs. Giving these features away creates a massive viral moat against legacy competitors.
*   **Free Tier**: 
    *   Unobtrusive Google AdMob banner integration.
    *   Full access to unlimited batch processing, Edge AI vision filtering, and content-aware downscaling.
*   **Shrinker Premium (Google Play Subscription)**:
    *   **Ad-Free Experience**: Completely removes all AdMob placements.
    *   **Advanced AI Workflows**: Unlocks multi-step, complex NLP chains (e.g., "Shrink this video to 50MB, extract the audio to MP3, and transcribe").
    *   **Aesthetic Customization**: Unlocks premium dark mode variants, custom app icons, and "Sleek Interface" color palettes.

## 5. Success Metrics (KPIs)
*   **Storage Reclaimed**: Total megabytes saved globally across user base (a great vanity metric for marketing).
*   **Processing Success Rate**: Percentage of media files successfully transcoded without out-of-memory or codec failure crashes.
*   **Retention**: Day 7 and Day 30 Active Users.
*   **Conversion Rate**: Free-to-Pro upgrade percentage.
