# ELLIE-CHATBOT
Ellie Chat App

A hybrid Android chat application using the RunAnywhere SDK for on-device inference plus the Perplexity API for online model access.

What this app does

Ellie Chat enables conversations with your chatbot “Ellie” through two modes:

On-device inference via RunAnywhere SDK: local models for low-latency, offline use.

Cloud inference via Perplexity API: when internet is available, route queries to the Perplexity API for higher-capacity model responses. 
Perplexity

The app automatically manages model download, load, and streaming generation.

Key features

Local model management: download, load, switch models on device.

Online fallback/integration: when connected, queries may use the Perplexity API endpoint.

Streaming responses: results generated word-by-word for interactive feel.

Jetpack Compose interface: clean UI for chat and model management.

Hybrid architecture: offline first, online fallback to Perplexity API.

Quick start

Build and run the app:

./gradlew assembleDebug


Or open in Android Studio and click Run.

Launch the app and go to “Models” section.

Download a model (e.g., “SmolLM2 360M Q8_0”).

Tap “Load” after download completes.
Wait until “Ellie is ready to chat!” appears.

Type messages and hit Send.

If offline: the on-device model handles inference.

If online: Ellies system may call the Perplexity API for improved responses.

Model availability
Model	Size	Quality	Best for
SmolLM2 360M Q8_0	~119 MB	Basic quality, fast	Offline quick replies
Qwen 2.5 0.5B Instruct Q6_K	~374 MB	Higher quality	General conversations
Technical details

SDK components: RunAnywhere Core SDK (model management + inference)

Perplexity API integration: Uses Perplexity’s API endpoint (compatible with OpenAI’s Chat Completions format) 
Perplexity

Architecture:

MyApplication.kt — initialization of SDK, registration of local models + API key for Perplexity.

ChatViewModel.kt — orchestrates chatting logic, chooses local vs online model, streams responses.

MainActivity.kt (Compose UI) — chat screen, model selection UI.

Hybrid logic: On user input → check connectivity → if online & flagged → send to Perplexity API → receive response → stream to UI; else run local model.

Requirements

Android 7.0 (API 24) or higher

~200 MB free storage (for smallest model)

Internet connection (for cloud mode via Perplexity)

Permission: INTERNET in AndroidManifest.xml

Troubleshooting

Models not appearing: Wait a few seconds after launch, tap “Refresh”.

Download fails: Check internet and storage space. Verify INTERNET permission.

App crashes during generation: Try smaller model, enable largeHeap="true" in manifest.

Slow generation: On-device models have performance limits--that’s expected. Use smaller model for speed.

Next steps / Customization

Add more local models (MyApplication.kt → registerModels()).

Change UI design (in MainActivity.kt).

Persist chat history (use Room or DataStore).

Add model-parameter tuning (temperature, top-k, top-p).

Configure how/when Ellie defaults to Perplexity API (e.g., use cloud for long conversations).

Extend cloud logic: pass user profile/context to Perplexity API, configure sources, etc.

Perplexity API notes

The Perplexity API supports the OpenAI chat completions format, making integration easier. 
Perplexity

You’ll need to manage your API key (via Perplexity dashboard) and monitor usage. 
Perplexity AI

Ensure you design fallback logic so that if the API fails or network drops, the local model kicks in.

License

This project follows the license terms of the RunAnywhere SDK and the Perplexity API. Include their respective licenses in your project.
