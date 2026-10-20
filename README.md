# HINA

HINA (Hyper-Interactive Neural Assistant) is a desktop voice and chat companion for study support, planning, everyday questions, and computer tasks. The showcase repository documents the project; the executable application lives in [HINA-Core](https://github.com/BogguAjayKumar/HINA-Core).

> Project status: active development. Capabilities depend on the local machine, installed models, and configured integrations.

## What HINA can do

- Chat through a native desktop window or use the voice assistant.
- Listen to personal stories, respond conversationally, explain new topics, and help make realistic study plans.
- Offer study prompts, active-recall quizzes, and focus timers.
- Keep conversation history locally and save long-term facts only when the user asks and approves the save.
- Use tools for supported desktop, file, reminder, web, email, calendar, and smart-home tasks, with an approval step before consequential actions or external requests.
- Use a local Ollama model by default. Cloud reasoning providers are optional.

See the [core repository README](https://github.com/BogguAjayKumar/HINA-Core#readme) for current setup and launch instructions.

## Privacy and action approvals

- HINA defaults to local-only reasoning with Ollama on this computer. In that mode, it refuses a non-loopback Ollama endpoint and does not fall back to a cloud LLM.
- Setting `HINA_LOCAL_ONLY=false` opts into configured cloud reasoning. Chat content may then be sent to the selected provider. The chat window shows the configured mode.
- External lookups and actions that can share information or change state require explicit approval before they run. Review the details and approve or cancel each request.
- Conversations and saved facts are stored in a local SQLite database. HINA does not encrypt that database. The clear-data control removes chat history and saved facts; it does not delete notes, reminders, lists, or files.
- Voice input is transcribed locally when using the bundled Faster-Whisper path. Optional integrations such as Edge TTS may communicate with their service; choose and configure integrations with that data flow in mind.

These controls reduce unintended sharing and actions, but local storage is still accessible to software running under the same Windows account.

## Repositories

- [HINA-Core](https://github.com/BogguAjayKumar/HINA-Core): application source code and setup instructions.
- [HINA-Showcase](https://github.com/BogguAjayKumar/HINA-Showcase): project overview and architecture notes.