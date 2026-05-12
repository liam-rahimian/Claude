# Gemini integration with Claude Code CLI

The objective of this setup is to use Claude Code’s orchestration layer, such as its multi-step agent loop, to help AI models like Gemini perform better and handle more complex tasks. Claude Code manages the orchestration and execution flow, while Gemini handles the actual text generation.

<img width="720" height="280" alt="agentic-loop" src="https://github.com/user-attachments/assets/b54e8d1b-10c4-41a4-b85f-84aa43bb954e" />



## 1. Install Claude Code

https://docs.anthropic.com/en/docs/claude-code

```bash
curl -fsSL https://claude.ai/install.sh | bash
```
---

## 2. Install Claude Code Router

https://github.com/musistudio/claude-code-router

```bash
npm install -g @musistudio/claude-code-router
```

Verify:

```bash
ccr --version
```

---

## 5. Create a Gemini API Key

https://aistudio.google.com/app/apikey

Generate a Gemini API key.

---

## 6. Add Your Gemini API Key

Open shell config:

```bash
nano ~/.zshrc
```

Add:

```bash
export GEMINI_API_KEY="YOUR_API_KEY"
```

Reload shell:

```bash
source ~/.zshrc
```

Verify:

```bash
echo $GEMINI_API_KEY
```

---

## 7. Configure Claude Code Router

Create/open config:

```bash
nano ~/.claude-code-router/config.json
```

Paste:

```json
{
  "LOG": true,
  "GEMINI_API_KEY": "$GEMINI_API_KEY",
  "Providers": [
    {
      "name": "gemini",
      "api_base_url": "https://generativelanguage.googleapis.com/v1beta/models/",
      "api_key": "$GEMINI_API_KEY",
      "models": ["gemini-2.5-flash"],
      "transformer": {
        "use": ["gemini"]
      }
    }
  ],
  "Router": {
    "default": "gemini,gemini-2.5-flash"
  }
}
```

---

## 8. Restart Claude Code Router

After changing config:

```bash
ccr restart
```

## 9. Launch Claude Code Through Router

```bash
ccr code
```

Now you are using:

- Claude Code orchestration
- Gemini as the backend model

---

## 11. Useful Commands

### Restart router

```bash
ccr restart
```

### Stop router

```bash
ccr stop
```

### Router status

```bash
ccr status
```

