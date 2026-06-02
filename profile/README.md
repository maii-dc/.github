# 🐄 Mai — cozy community systems

> Make your server feel like home.

Mai is a warm, mood-driven Discord bot with a custom greeter system and ticket system. Every message is styled by your server's active **mood** — from a lofi café to a midnight city.

---

## ✨ Features

| Feature | Description |
|---|---|
| 🎉 Welcome Greeter | Sends a mood-flavoured embed when a member joins |
| 🎫 Ticket System | Private ticket channels with open/close buttons |
| 🌙 Mood System | 5 moods that style all of Mai's embeds and wording |
| ⚙️ Per-Server Config | Each server's settings are stored in their own JSON file |

---

## 🚀 Setup

### 1. Prerequisites

- **Node.js v18+** — [download](https://nodejs.org/)
- A Discord bot application — [create one here](https://discord.com/developers/applications)

### 2. Bot Permissions

When inviting Mai, make sure she has these permissions:
- `Manage Channels` (to create ticket channels)
- `Send Messages`
- `Read Message History`
- `Embed Links`
- `Manage Roles` *(if you want her to set permissions on ticket channels)*

Also enable the **Server Members Intent** in your bot's settings page (under *Privileged Gateway Intents*).

### 3. Install & Configure

```bash
# Clone or download the project
cd mai-bot

# Install dependencies
npm install

# Copy the example env file
cp .env.example .env
```

Open `.env` and fill in:

```env
DISCORD_TOKEN=your_bot_token_here
CLIENT_ID=your_client_id_here
GUILD_ID=your_test_guild_id_here   # optional but recommended during setup
```

### 4. Deploy Slash Commands

```bash
npm run deploy
```

This registers all slash commands. If `GUILD_ID` is set, they appear instantly. Without it, global deployment can take up to an hour.

### 5. Start the Bot

```bash
npm start
```

You should see:
```
🐄  Mai is online — logged in as Mai#1234
   Serving 1 guild(s)
```

---

## 🛠️ Commands

| Command | Permission | Description |
|---|---|---|
| `/setup welcome` | Manage Guild | Set the welcome channel and message |
| `/setup tickets` | Manage Guild | Set the ticket category and support role |
| `/mood set` | Manage Guild | Change the server's active mood |
| `/ticketpanel` | Manage Guild | Post the ticket panel in the current channel |

### `/setup welcome`

| Option | Required | Description |
|---|---|---|
| `channel` | ✅ | Text channel for welcome messages |
| `message` | ❌ | Custom message — use `{user}` for a mention |

### `/setup tickets`

| Option | Required | Description |
|---|---|---|
| `category` | ✅ | Category where ticket channels are created |
| `support_role` | ✅ | Role that can see and respond to tickets |
| `transcript_channel` | ❌ | Channel to log closed tickets (future feature) |

### `/mood set`

Choose from:

| Key | Name | Vibe |
|---|---|---|
| `lofi-cafe` | ☕ Lofi Café | warm, cozy, latte energy |
| `rainy-night` | 🌧️ Rainy Night | calm, introspective |
| `winter-cabin` | 🪵 Winter Cabin | fireplace, hygge |
| `midnight-city` | 🌃 Midnight City | neon, urban, night owl |
| `study-session` | 📖 Study Session | focused, productive, sage |

---

## 📁 Data Storage

Each server's config is stored in:

```
src/data/guilds/<GUILD_ID>.json
```

These files are created automatically when you run `/setup`. No database required.

---

## 🧩 Project Structure

```
mai-bot/
├─ src/
│  ├─ index.js              # Bot entry point
│  ├─ deploy-commands.js    # Slash command registration
│  ├─ config.js             # Bot-wide constants
│  ├─ commands/
│  │  ├─ setup.js           # /setup welcome & tickets
│  │  ├─ mood.js            # /mood set
│  │  └─ ticketpanel.js     # /ticketpanel
│  ├─ events/
│  │  ├─ ready.js           # Bot startup
│  │  ├─ guildMemberAdd.js  # Member join
│  │  └─ interactionCreate.js # All interactions
│  ├─ systems/
│  │  ├─ greeter.js         # Welcome logic
│  │  ├─ tickets.js         # Ticket open/close logic
│  │  └─ moods.js           # Mood definitions
│  ├─ data/guilds/          # Per-server JSON configs
│  └─ utils/
│     ├─ loadConfig.js
│     ├─ saveConfig.js
│     └─ embeds.js
├─ .env.example
├─ package.json
└─ README.md
```

---

## 💡 Tips

- Run `npm run deploy` again any time you add a new command.
- Delete a server's JSON file to reset its config to defaults.
- Set `GUILD_ID` during development for instant command updates; remove it for production global deployment.

---

*Mai — make your server feel like home.* 🐄
