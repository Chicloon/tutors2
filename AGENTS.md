# Video Chat MVP

## Overview
Video conferencing MVP: 1-on-1 video calls + real-time chat. Localhost only.

## Stack

| Layer | Technology |
|-------|------------|
| Frontend | React 18 + TypeScript + Vite |
| Backend | Node.js + Express + Socket.io |
| Database | SQLite (better-sqlite3) |
| Auth | JWT |
| Video | WebRTC P2P (Socket.io signaling) |

## Project Structure

```
/
├── server/
│   ├── src/
│   │   ├── index.ts
│   │   ├── db.ts
│   │   ├── auth.ts
│   │   └── routes/
│   │       ├── auth.ts
│   │       └── rooms.ts
│   └── package.json
└── client/
    ├── src/
    │   ├── App.tsx
    │   ├── pages/
    │   │   ├── Login.tsx
    │   │   ├── Dashboard.tsx
    │   │   └── Room.tsx
    │   ├── components/
    │   │   ├── VideoPlayer.tsx
    │   │   ├── Chat.tsx
    │   │   └── Controls.tsx
    │   ├── hooks/
    │   │   └── useWebRTC.ts
    │   └── services/
    │       └── api.ts
    └── package.json
```

## Phases

### Phase 1: Backend (1 day)
1. Express + TypeScript setup
2. SQLite tables: users, rooms, messages
3. REST: POST /api/register, POST /api/login, GET/POST /api/rooms
4. Socket.io events: join-room, leave-room, chat-message, offer, answer, ice-candidate

### Phase 2: Frontend (1-2 days)
1. Vite + React + TypeScript setup
2. Login/Register page
3. Dashboard: room list + create room button
4. Room page: 2 videos + chat + controls

### Phase 3: WebRTC (1 day)
1. useWebRTC hook — RTCPeerConnection
2. Offer/answer exchange via Socket.io
3. ICE candidates via Socket.io
4. getUserMedia for local stream

### Phase 4: Chat (0.5 day)
1. Socket.io chat events
2. Store messages in SQLite
3. UI: message list + input

## Socket Events
- `join-room` — user enters room
- `leave-room` — user leaves room
- `user-joined` / `user-left` — room state
- `offer` / `answer` / `ice-candidate` — WebRTC signaling
- `chat-message` — send message

## Database Schema

### Users
- id (PK), username, password_hash, created_at

### Rooms
- id (PK), host_id (FK users), created_at, is_active

### Messages
- id (PK), room_id (FK rooms), sender_id (FK users), content, created_at

## Environment Variables

### Server
```
PORT=3001
JWT_SECRET=<secret>
DATABASE_PATH=./data/app.db
```

### Client
```
VITE_API_URL=http://localhost:3001/api
VITE_WS_URL=ws://localhost:3001
```

## Run
```bash
cd server && npm run dev   # localhost:3001
cd client && npm run dev   # localhost:5173
```

## Success Criteria
- [ ] Register/Login works
- [ ] Create/join room by ID
- [ ] Video + audio between 2 users
- [ ] Real-time text chat
- [ ] Controls: mute, camera off, leave
