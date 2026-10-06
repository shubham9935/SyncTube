# SyncTube

SyncTube is a real-time YouTube watch-party app. Create a room, invite friends, and watch together with synchronized playback, chat, reactions, and a shared playlist.

## Screenshots

The screenshots below show the app at phone, tablet, and desktop sizes. Room images use the empty-player state so the room layout and controls remain visible.

### Home page

| Phone · 390 × 844 | Tablet · 834 × 1112 | Desktop · 1440 × 900 |
|---|---|---|
| <img src="client/public/screenshots/readme/home-phone.png" alt="SyncTube home page on a phone" width="260"> | <img src="client/public/screenshots/readme/home-tablet.png" alt="SyncTube home page on a tablet" width="260"> | <img src="client/public/screenshots/readme/home-desktop.png" alt="SyncTube home page on a desktop" width="360"> |

### Home page guides

| How it works | Feature overview |
|---|---|
| <img src="client/public/screenshots/readme/home-how-it-works.png" alt="How SyncTube works guide" width="480"> | <img src="client/public/screenshots/readme/home-features.png" alt="SyncTube feature overview" width="480"> |

### Watch room

| Phone · 390 × 844 | Tablet · 834 × 1112 | Desktop · 1440 × 900 |
|---|---|---|
| <img src="client/public/screenshots/readme/room-phone.png" alt="SyncTube watch room on a phone, with mobile playback controls and scrollable room tabs" width="260"> | <img src="client/public/screenshots/readme/room-tablet.png" alt="SyncTube watch room on a tablet" width="260"> | <img src="client/public/screenshots/readme/room-desktop.png" alt="SyncTube watch room on a desktop, with the video stage and participants panel" width="360"> |

### Room tabs and activity

| Participants | Playlist | Chat |
|---|---|---|
| <img src="client/public/screenshots/readme/room-participants.png" alt="Participants list with the host role badge" width="360"> | <img src="client/public/screenshots/readme/room-playlist.png" alt="Shared Up Next playlist with a queued video" width="360"> | <img src="client/public/screenshots/readme/room-chat.png" alt="Room chat with a message and reply-capable composer" width="360"> |

| Action requests | Activity |
|---|---|
| <img src="client/public/screenshots/readme/room-requests.png" alt="Host action requests panel" width="360"> | <img src="client/public/screenshots/readme/room-activity.png" alt="Room activity feed showing join and connection events" width="360"> |

### Search, invitations, and settings

| YouTube search | Invite friends |
|---|---|
| <img src="client/public/screenshots/readme/search.png" alt="YouTube video search with a result and queue actions" width="480"> | <img src="client/public/screenshots/readme/invite.png" alt="Invite dialog with a QR code, room code, and sharing links" width="480"> |

| User settings | Room settings |
|---|---|
| <img src="client/public/screenshots/readme/settings-user.png" alt="User settings for anime avatar, display name, color, and ambient mode" width="480"> | <img src="client/public/screenshots/readme/settings-room.png" alt="Room settings for appearance, roles, permissions, playlist, and chat" width="480"> |

The invite screenshot shows a sample room code and development link. Create an invite in the live app to get a link for your own room.

## Deployment

The app has a React/Vite frontend hosted on Vercel and an Express/Socket.IO backend hosted on Render. The root [`vercel.json`](./vercel.json) builds the frontend and forwards API and Socket.IO requests to the Render service. [`render.yaml`](./render.yaml) defines the backend service.

### Render

1. In Render, create a **Blueprint** from this GitHub repository and select `render.yaml`.
2. Set `FRONTEND_URL` to the deployed Vercel site URL.
3. Optionally set `DATABASE_URL` to a PostgreSQL connection string. Without it, room state is held in memory and is lost when the server restarts.
4. Deploy the service and confirm its `/health` endpoint responds.

### Vercel

1. Import this GitHub repository into Vercel.
2. Keep the project root at the repository root so Vercel uses `vercel.json`.
3. Deploy after the Render backend is available. The rewrite destinations in `vercel.json` must point to the public Render service URL.

Both hosting services can be configured to deploy from the `main` branch.

## Local development

Requirements: Node.js and npm.

```sh
npm ci
npm run dev
```

Build both apps with `npm run build`. Run the test suites with `npm test`.

## Data and configuration

The server uses PostgreSQL through the optional `DATABASE_URL` setting to persist basic room playback metadata. Without a database, rooms run in memory. Chat, playlists, polls, reactions, and participant presence are also in-memory and are not durable across server restarts. Browser settings and recent-room history are stored locally in the user's browser.

Do not commit `.env` files, database connection strings, or other secrets. Production environment variables should be set in the Render or Vercel project settings as appropriate.
