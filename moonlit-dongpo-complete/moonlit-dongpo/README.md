# 月下东坡 · Gemini Free-Tier Edition

A jade-green and gold Chinese poetry chatbot focused on 苏轼《水调歌头》.

## Windows quick start

1. Install Go 1.23 or newer.
2. Extract the ZIP and open the inner `moonlit-dongpo` folder in VS Code.
3. Copy `.env.example` to `.env` in the same folder as `main.go`.
4. Create a Gemini API key in Google AI Studio: https://aistudio.google.com/apikey
5. In `.env`, replace `PASTE_YOUR_GEMINI_KEY_HERE` with your key.
6. Double-click `start-windows.bat`, or run `go run .` in that folder.
7. Open http://localhost:8081 in a browser.

**Do not put the key in web/ files or share/commit your `.env` file.**

### VS Code PowerShell commands

```powershell
Copy-Item .env.example .env
notepad .env
# After saving your key:
go run .
```

### Configuration

- `GEMINI_API_KEY`: required for AI chat
- `GEMINI_MODEL`: defaults to `gemini-2.5-flash-lite`
- `PORT`: defaults to `8080`, but `.env.example` sets `8081`

The website and API run in the same Go process. `POST /api/chat` retains the original request/response contract, session pacing, validation, and recent-message history. The browser never sees the API key.

### Troubleshooting

- **Website works, AI doesn't:** inspect the server terminal for `Gemini request failed:`.
- **HTTP 400:** bad request/model configuration.
- **HTTP 401/403:** invalid or unauthorized key/project.
- **HTTP 404:** model name not available to your project; check available models in AI Studio.
- **HTTP 429:** free-tier rate limit or quota reached.
- **HTTP 503:** service unavailable.
- **Address already in use:** stop the other Go server or set another `PORT` in `.env`.

### Hosting

On Render, build with `go build -o app .` and start with `./app`.
Set `GEMINI_API_KEY` as a secret environment variable on Render, and optionally `GEMINI_MODEL`.
The host sets `PORT`. Do not upload `.env` to GitHub.

**Free-tier limitations:** Gemini API free-tier availability, usage limits, and eligible models may change. Free-tier inputs and outputs may be used to improve Google's products. Avoid submitting personal or sensitive information. Hosting a publicly accessible site may require a paid hosting plan even if model requests remain within free-tier limits.
