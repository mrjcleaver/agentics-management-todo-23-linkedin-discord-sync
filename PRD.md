# 🧾 PRD: Discord–LinkedIn Real Name Sync Bot

## 🧭 Overview

A Discord bot that verifies user identity via LinkedIn OAuth and updates the user's server nickname to match their LinkedIn profile name. This helps server admins maintain professionalism, transparency, and identity consistency within the community.

---

## 🎯 Goals

- Enforce that users in a Discord server use their real names as displayed on LinkedIn.
- Allow seamless identity verification through LinkedIn login.
- Automatically or manually update the user’s server nickname.
- Ensure user privacy and consent are respected.

---

## 🔑 Features

### 1. LinkedIn OAuth Verification

- Prompt users to verify their identity by logging into LinkedIn via OAuth 2.0.
- Request basic profile data (`r_liteprofile`):
  - `firstName.localized.en_US`
  - `lastName.localized.en_US`
  - `profilePicture` (optional)

### 2. Nickname Synchronization

- After verification:
  - Fetch the user's real name.
  - Update their **server nickname** (not global username) to: `FirstName LastName`
- Handle errors (e.g., nickname too long, permissions, API issues).

### 3. Verification Status Tracking

- Store verified mappings of LinkedIn → Discord ID in a database.
- Allow re-verification or updates.

### 4. Admin Tools

- `/verify @user` – Prompt a specific user to verify.
- `/refresh-name @user` – Refresh Discord nickname from LinkedIn.
- `/verified-list` – View a list of verified users.

### 5. User Commands

- `/verify` – Start the LinkedIn verification flow.
- `/unlink` – Remove LinkedIn linkage (with a warning about nickname reversion).

---

## 🚦 User Journey

1. User joins server.
2. Bot greets user in DMs or a welcome channel.
3. User decides that they want to become a verified user
4. User runs `/verify` and is sent to a LinkedIn OAuth link.
5. User authorizes the app.
6. Bot fetches LinkedIn name and updates server nickname.
7. Mapping is saved for future reference.
8. Role "identify verified by LinkedIn" is added by bot
9. Periodically, verified users server nickname is checked against the saved mapping 
---

## 🛠️ Technical Specifications

- **Discord Bot Framework**: discord.py / discord.js
- **OAuth Provider**: LinkedIn Developer App (OAuth 2.0)
- **Database**: SQLite, Supabase, or PostgreSQL

### Required Permissions

- `MANAGE_NICKNAMES`
- `SEND_MESSAGES`
- `USE_APPLICATION_COMMANDS`

### LinkedIn API Scopes

- `r_liteprofile`

---

## ✅ Acceptance Criteria

| Requirement               | Acceptance Test                                        |
|---------------------------|--------------------------------------------------------|
| Verify via LinkedIn       | `/verify` initiates OAuth, bot receives profile name  |
| Nickname is updated       | User’s nickname becomes `First Last`                  |
| Mapping is stored         | User appears in `/verified-list`                      |
| Unlinking is supported    | `/unlink` deletes saved mapping                       |
| Manual refresh works      | `/refresh-name` updates nickname if profile changes   |

---

## 📦 Nice-to-Haves (v2)

- Assign roles based on LinkedIn headline or company.
- Display LinkedIn profile link in `/whois`.
- Optionally suggest nickname instead of enforcing it.
- Support GitHub, Google, or Twitter as alternate verification.

---

## ⚠️ Constraints & Risks

- LinkedIn API rate limits and strict review process.
- Must obtain explicit user consent before updating nicknames.
- Handle edge cases: long names, Unicode, duplicate names.

---

## 🔗 Integrations

- Discord API
- LinkedIn OAuth
- Optional: Pipedream, n8n, Firebase, Supabase

---

## 📅 Timeline Estimate

| Phase                | Deliverable                                | Time    |
|----------------------|---------------------------------------------|---------|
| Planning & Setup     | Repo, LinkedIn app, bot scaffold            | 1 week  |
| OAuth Flow           | LinkedIn login and token handling           | 1 week  |
| Discord Commands     | Slash commands, nickname update logic       | 1 week  |
| Persistence & Admin  | Store mappings, admin tools                 | 1 week  |
| Testing & Launch     | Internal test, review, deploy               | 1 week  |

---

Please 👍 or comment if you're interested in contributing!
