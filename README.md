# OpenRouter Responses API Chat

A single-file HTML chat interface for [OpenRouter's Responses API](https://openrouter.ai/docs/api/reference/responses/overview). Access 400+ AI models through a unified, modern streaming API with advanced features like reasoning, tool calling, and multi-model conversations.

**Live Demo:** [https://mbbrinkman.github.io/ResponsesAPIChat/responses.html](https://mbbrinkman.github.io/ResponsesAPIChat/responses.html)

## Features

### Multi-Model Support
- **Parallel Mode**: All selected models respond independently to your message
- **Serial Mode**: Models respond one after another, seeing all previous responses
- **Rotating Mode**: Like Serial, but order rotates each turn
- **Autonomous Mode**: Models converse with each other without human input

### Advanced Capabilities
- **Extended Thinking/Reasoning**: Enable chain-of-thought reasoning for supported models (O1, Claude, etc.)
- **Tool Calling**: Define custom functions for models to invoke
- **Structured Output**: Force JSON mode or JSON schema output
- **Provider Routing**: Control which providers handle your requests with price limits, latency preferences, and more
- **Plugins**: Web search, file parsing, moderation, and response healing

### Conversation Management
- Edit AI responses before continuing
- Regenerate responses with the same or different model
- Continue responses that were cut off
- Prefill mode to guide response style
- Role switching (convert user ↔ assistant messages)
- Edit names of participants

### File Attachments
- **Images**: Sent as visual data to vision-capable models
- **PDFs**: Text content automatically extracted
- **Text files**: Content read and sent to model
- Image generation support for compatible models

### Data Storage
- All data stored locally in IndexedDB (50MB to several GB)
- Export/import all settings and conversations
- Conversation history with save/load
- Mobile-friendly with reliable storage

## Quick Start

1. Open [responses.html](https://mbbrinkman.github.io/ResponsesAPIChat/responses.html) in your browser
2. Go to **Settings** → Add your [OpenRouter API key](https://openrouter.ai/keys)
3. Click **Load Models** to browse available models
4. Click any model to auto-populate the configuration
5. **Select Models** → choose which models to use
6. Start chatting!

## Model Configuration

Each model is configured with JSON (without outer braces):

```json
"endpoint": "https://openrouter.ai/api/v1/responses",
"model_id": "anthropic/claude-3.5-sonnet",
"api_key_id": "your-saved-key-id",
"system_prompt": "",
"max_output_tokens": null,
"temperature": 1.0,
"top_p": null,
"top_k": null,
"frequency_penalty": null,
"presence_penalty": null,
"seed": null,
"stop": null,
"tools": null,
"tool_choice": null,
"parallel_tool_calls": null,
"reasoning": null,
"text": null,
"user": null,
"session_id": null,
"store": null,
"metadata": null,
"provider": null,
"plugins": null,
"timeout": 120000
```

### Key Parameters

| Parameter | Description |
|-----------|-------------|
| `temperature` | 0.0-2.0, controls randomness |
| `max_output_tokens` | Maximum response length |
| `top_p` / `top_k` | Nucleus/top-k sampling |
| `reasoning` | Extended thinking config: `{"effort": "high"}` |
| `text` | Output format: `{"format": {"type": "json_object"}}` |
| `tools` | Function definitions for tool calling |
| `provider` | Routing preferences, price limits |
| `plugins` | Web search, moderation, etc. |
| `timeout` | Request timeout in ms (default: 120000) |

### Example: Enable Reasoning

```json
"reasoning": {"effort": "high", "summary": "detailed"}
```

### Example: JSON Mode

```json
"text": {"format": {"type": "json_object"}}
```

### Example: Provider Routing

```json
"provider": {
  "sort": "price",
  "max_price": {"prompt": 0.5, "completion": 1.5},
  "zdr": true
}
```

### Example: Web Search Plugin

```json
"plugins": [{"id": "web", "max_results": 5}]
```

## Supported Models

Access 400+ models through OpenRouter including:

- **Anthropic**: Claude 3.5 Sonnet, Claude 3 Opus, Claude 3 Haiku
- **OpenAI**: GPT-4o, GPT-4, O1, O1-mini
- **Google**: Gemini Pro, Gemini Ultra
- **Meta**: Llama 3, Llama 3.1
- **Mistral**: Mixtral, Mistral Large
- **And many more** at [openrouter.ai/models](https://openrouter.ai/models)

## Self-Hosting

This is a single HTML file with no build process required:

1. Download `responses.html`
2. Open in any modern web browser
3. All data is stored locally in your browser

Or serve it from any static file host (GitHub Pages, Netlify, Vercel, etc.).

## Privacy

- All data stays in your browser (IndexedDB)
- Only API calls go to OpenRouter
- No analytics or tracking
- No server-side storage (unless you enable `store: true`)

## License

**CC0 (Public Domain)** - Do whatever you want with this code. No attribution required.

## Links

- [OpenRouter](https://openrouter.ai) - API provider
- [OpenRouter Docs](https://openrouter.ai/docs) - API documentation
- [Get API Key](https://openrouter.ai/keys) - Create your key
- [Browse Models](https://openrouter.ai/models) - See all available models
