# Chaster.App Telegram Bot

A Telegram bot that integrates with [chaster.app](https://chaster.app)'s API to let group members affect each other's lock times using emoji reactions.

## 🧠 Project Overview

The goal of this project is to build a Telegram bot that can be added to group chats. The bot listens for emoji reactions on messages and adjusts a user’s Chaster lock time based on group feedback:

- ❤️ = Decrease lock time
- 👎 = Increase lock time

For example:
- User A says something funny → someone reacts with ❤️ → lock time decreases.
- User B says something unfunny → someone reacts with 👎 → lock time increases.

Reactions can be configured per-chat to allow group-specific rules.

## 🔧 Features

- ✅ Emoji reaction tracking for messages  
- ✅ Integration with Chaster’s public API  
- ✅ Per-chat emoji configuration  
- ✅ Per-user OAuth authentication  
- ✅ Secure lock time changes through Chaster’s API  
- **Rate limiting and anti-abuse mechanisms** - This bot is intended to be fun, chaotic, and consensual — not miserable. The following anti-abuse ideas are designed to keep it playful without letting things get out of hand
  - 🟡 **Consensus mode**: After the first reaction, a 15-minute window collects votes; the net outcome determines one-time lock adjustment  
  - 🟡 **24-hour reaction validity**: Only count reactions placed within 24 hours of a message  
  - 🟡 **Per-reactor rate limits**: Limit how often a user can affect others’ locks  
  - 🟡 **Consensus per user**: Each user can only have one active "under review" message at a time  
  - 🟡 **Reaction intent detection**: If one person reacts to many of another user’s messages in a short time, only their dominant sentiment is counted  
  - 🟡 **Lock change caps**: Prevent drastic changes to a user’s lock in one day (e.g. ±15 min per day max)  
  - 🟡 **Message cooldown**: Only allow a limited number of actionable messages per user per hour  
- 🟡 Admin commands to configure emoji mappings, increment values, and caps per chat  

## 🔐 Authentication with Chaster

Users will need to authorize the bot to make changes to their lock via OAuth2. Chaster’s API supports OAuth2 token flows for accessing and modifying user data. See:

- [OAuth Flow](https://docs.chaster.app/api/oauth/oauth-flow/)
- [Getting User Info](https://docs.chaster.app/api/users/get-current-user/)
- [Modifying a Lock](https://docs.chaster.app/api/locks/update-lock/)

## 📚 Useful API Endpoints

Here are some likely starting points from Chaster’s API:

- 🔒 **GET User Locks**  
  `GET /api/locks`  
  Retrieve all current locks to find the active one.

- 🔁 **PATCH Update Lock Time**  
  `PATCH /api/locks/{id}`  
  Modify the `end_date` or duration based on emoji reactions.

- 👤 **GET Current User**  
  `GET /api/users/me`  
  To verify identity after OAuth.

- 🔑 **OAuth Flow**  
  See: https://docs.chaster.app/api/oauth/oauth-flow/  
  For authorizing users and storing tokens securely.

## 🚧 Roadmap

- [ ] Telegram Bot API integration
- [ ] OAuth integration with Chaster
- [ ] Emoji-to-action mapping per chat
- [ ] Rate limiting (per-reactor and per-target)
- [ ] Daily lock change caps
- [ ] Reaction validity window enforcement (24hr)
- [ ] Consensus window (15 min, vote tallying)
- [ ] Abuse mitigation for reaction spamming
- [ ] Admin configuration commands
- [ ] Deploy bot and create usage docs

## 🐾 Contributing

Pull requests and issue reports are welcome! But please be nice, I'm an IT professional with a hobby, not a programmer by trade.

---

> This is a personal project and is not affiliated with Chaster.app or Telegram.
