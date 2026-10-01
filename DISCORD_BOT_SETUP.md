# Discord Bot Setup Guide

This is a complete Discord.js bot template with command handler, slash commands, and configuration.

## Prerequisites

- Node.js v16.0.0 or higher
- npm or yarn
- A Discord server for testing

## Step 1: Create a Discord Application

1. Go to [Discord Developer Portal](https://discord.com/developers/applications)
2. Click "New Application"
3. Give your bot a name and click "Create"
4. Go to the "Bot" tab on the left
5. Click "Add Bot"
6. Under the bot name, click "Reset Token" and copy it
7. Go to "OAuth2" → "URL Generator"
8. Select scopes: `bot` and `applications.commands`
9. Select permissions: 
   - `Send Messages`
   - `Read Message History`
   - `View Channels`
10. Copy the generated URL and open it in your browser to invite the bot to your server

## Step 2: Set Up Environment Variables

1. Copy `.env.example` to `.env`:
   ```bash
   cp .env.example .env
   ```

2. Fill in the `.env` file with your credentials:
   ```env
   DISCORD_TOKEN=your_bot_token_here
   CLIENT_ID=your_client_id_here
   GUILD_ID=your_guild_id_here
   ```

   Where:
   - **DISCORD_TOKEN**: Bot token from Developer Portal → Bot section
   - **CLIENT_ID**: Application ID from Developer Portal → General Information
   - **GUILD_ID**: Your Discord server ID (Enable Developer Mode in Discord settings, right-click server → Copy Server ID)

## Step 3: Install Dependencies

```bash
npm install
```

## Step 4: Deploy Slash Commands

Before running the bot for the first time, register the slash commands:

```bash
node deploy-commands.js
```

You should see:
```
Started refreshing X application (/) commands.
Successfully reloaded X application (/) commands.
```

## Step 5: Run the Bot

```bash
npm start
```

Or for development with auto-reload:
```bash
npm run dev
```

You should see:
```
✅ Bot logged in as YourBotName#0000
```

## Step 6: Test Your Bot

In your Discord server, type:

- `/ping` - Bot responds with latency information
- `/hello` - Bot greets you with a friendly message

## Adding New Commands

1. Create a new file in the `commands/` folder (e.g., `commands/mycommand.js`):

```javascript
const { SlashCommandBuilder } = require('discord.js');

module.exports = {
  data: new SlashCommandBuilder()
    .setName('mycommand')
    .setDescription('Description of your command'),
  async execute(interaction) {
    await interaction.reply('Your response here!');
  },
};
```

2. Deploy commands again:
```bash
node deploy-commands.js
```

3. Restart the bot

## Project Structure

```
discord-bot/
├── index.js                 # Main bot file
├── deploy-commands.js       # Script to register slash commands
├── package.json            # Dependencies
├── .env.example            # Environment variables template
├── .gitignore              # Git ignore rules
├── DISCORD_BOT_SETUP.md    # This file
└── commands/
    ├── ping.js             # Ping command
    └── hello.js            # Hello command
```

## Troubleshooting

### Bot doesn't respond to commands
- Make sure you ran `node deploy-commands.js`
- Check that GUILD_ID in `.env` is correct
- Restart the bot after deploying commands

### "Discord token is invalid"
- Double-check your token in `.env`
- Reset your bot token in Developer Portal

### "Bot doesn't appear in server"
- Make sure you used the OAuth2 URL to invite it
- Check that you selected `bot` scope and required permissions

## Resources

- [Discord.js Documentation](https://discord.js.org/)
- [Discord Developer Portal](https://discord.com/developers/applications)
- [Discord API Documentation](https://discord.com/developers/docs)

---

Happy botting! 🤖
