# opencode-discord-rpc

Discord Rich Presence plugin for [OpenCode](https://opencode.ai) - Show your AI-assisted coding activity in Discord!

![Discord Rich Presence Preview](https://via.placeholder.com/400x150?text=OpenCode+Rich+Presence)

## Features

- Shows your current AI model being used
- Displays session duration (elapsed time)
- Shows activity status (Coding/Idle/Thinking)
- Clickable button to visit OpenCode.ai
- Auto-reconnects if Discord restarts
- Zero configuration needed (uses default Discord App)

## Installation

### Prerequisites: Upload Rich Presence Assets

Before using the plugin, you need to upload image assets to your Discord Application:

1. Go to [Discord Developer Portal](https://discord.com/developers/applications/1462270555586822206/rich-presence/assets)
2. Click **"Add Image(s)"**
3. Upload the following assets (512x512 or 1024x1024 PNG):
   - `opencode_rp_large_dark_1024` - Main large image
   - `opencode_icon_tight_dark_1024` - Small status icon
4. Wait 5-10 minutes for Discord to process the assets

You can use the official OpenCode logo or any image you prefer.

### Option 1: Add to your OpenCode config (Recommended)

Add the plugin to your `opencode.json`:

```json
{
  "$schema": "https://opencode.ai/config.json",
  "plugin": ["opencode-discord-rpc"]
}
```

For global installation, add it to `~/.config/opencode/opencode.json`.

### Option 2: Install from npm

```bash
npm install opencode-discord-rpc
```

Then add `"opencode-discord-rpc"` to your config's plugin array.

## How It Works

Once installed, the plugin automatically:

1. Connects to Discord when OpenCode starts
2. Displays your current activity in Discord's Rich Presence
3. Updates in real-time as you code:
   - **Coding...** - When tools are executing or you're actively working
   - **Thinking...** - When the AI is generating a response
   - **Waiting for input...** - When the session is waiting for your input
   - **Idle** - When no session is active

## Rich Presence Display

```
┌─────────────────────────────────────────┐
│ [OpenCode Logo]                         │
│                                         │
│ Using claude-sonnet-4                   │
│ Coding...                               │
│ 01:23:45 elapsed                        │
│                                         │
│ [ Visit OpenCode.ai ]                   │
└─────────────────────────────────────────┘
```

## Configuration

The plugin works out of the box with sensible defaults. For advanced configuration, you can use environment variables:

| Variable | Description | Default |
|----------|-------------|---------|
| `OPENCODE_DISCORD_CLIENT_ID` | Custom Discord Application ID | `1462270555586822206` |
| `OPENCODE_DISCORD_ENABLED` | Set to `"false"` to disable | `"true"` |
| `OPENCODE_DISCORD_RETRY_INTERVAL` | Reconnect interval (ms) | `15000` |
| `OPENCODE_DISCORD_MAX_RETRIES` | Max reconnection attempts | `5` |

### Using a Custom Discord Application

If you want to use your own Discord Application (for custom branding):

1. Go to the [Discord Developer Portal](https://discord.com/developers/applications)
2. Click **"New Application"** and name it (e.g., "My OpenCode")
3. Copy the **Application ID** from the General Information page
4. Go to **Rich Presence > Art Assets**
5. Upload your images:
   - `opencode_rp_large_dark_1024` - Large image (512x512 or 1024x1024)
   - `opencode_icon_tight_dark_1024` - Small icon
6. Set the environment variable:
   ```bash
   export OPENCODE_DISCORD_CLIENT_ID="your-application-id"
   ```

## Requirements

- OpenCode v1.0+
- Discord Desktop App (must be running)
- Node.js 18+

## Troubleshooting

### Rich Presence not showing

1. **Make sure Discord is running** - The desktop app must be open
2. **Check Activity Status is enabled** - In Discord Settings > Activity Privacy, ensure "Display current activity as a status message" is ON
3. **Restart OpenCode** - The plugin connects on startup

### Connection errors in logs

The plugin will automatically retry if Discord isn't available. Common messages:

- `"Discord is not running or not accessible"` - Discord desktop app is closed
- `"Max retry attempts reached"` - Discord wasn't found after multiple attempts; restart OpenCode when Discord is running

### Privacy Concerns

This plugin does **not** display:
- Your project name or path
- File names or contents
- Any code or conversation content

It only shows:
- The AI model being used
- Your activity status (coding/idle)
- How long the session has been active

## Development

```bash
# Clone the repository
git clone https://github.com/yourusername/opencode-discord-rpc.git
cd opencode-discord-rpc

# Install dependencies
npm install

# Build
npm run build

# Watch mode for development
npm run dev
```

## License

MIT License - see [LICENSE](LICENSE) for details.

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## Credits

- Built for [OpenCode](https://opencode.ai)
- Uses [@xhayper/discord-rpc](https://github.com/xhayper/discord-rpc) for Discord IPC communication
- Inspired by [Discord-CustomRP](https://github.com/maximmax42/Discord-CustomRP)
