# AI Avatar Water Cooler Conversation - Complete Documentation

## Table of Contents
1. [Project Overview](#project-overview)
2. [Architecture](#architecture)
3. [Technology Stack](#technology-stack)
4. [System Components](#system-components)
5. [Setup Guide](#setup-guide)
6. [API Documentation](#api-documentation)
7. [UML Diagrams](#uml-diagrams)
8. [Features](#features)
9. [Troubleshooting](#troubleshooting)

---

## Project Overview

### Description
An interactive web application that enables users to have natural water cooler conversations with an AI-powered avatar named Jane Smith. The application supports both text and voice interactions, providing a realistic conversational experience using LiveAvatar's AI technology.

### Purpose
To create an engaging, human-like conversational interface that simulates casual workplace interactions, allowing users to practice social conversations or simply chat with a virtual colleague.

### Key Features
- Real-time AI avatar with lip-sync
- Text-based chat interface
- Voice input (Push-to-Talk and Continuous Voice Mode)
- Natural language processing
- Real-time transcription
- Responsive UI with message history

---

## Architecture

### High-Level Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                        Frontend (React)                      │
│  ┌────────────────┐  ┌──────────────┐  ┌─────────────────┐ │
│  │  AvatarChat    │  │  LiveKit     │  │  Voice Input    │ │
│  │  Component     │  │  Client      │  │  Handler        │ │
│  └────────────────┘  └──────────────┘  └─────────────────┘ │
└─────────────────────────────────────────────────────────────┘
                              │
                              │ HTTPS/WebSocket
                              ▼
┌─────────────────────────────────────────────────────────────┐
│                    Backend (Node.js/Express)                 │
│  ┌────────────────┐  ┌──────────────────────────────────┐  │
│  │  Session       │  │  LiveAvatar API Client           │  │
│  │  Controller    │  │  - Session Management            │  │
│  │                │  │  - Knowledge Base Integration    │  │
│  └────────────────┘  └──────────────────────────────────┘  │
└─────────────────────────────────────────────────────────────┘
                              │
                              │ REST API
                              ▼
┌─────────────────────────────────────────────────────────────┐
│                    LiveAvatar Platform                       │
│  ┌────────────────┐  ┌──────────────┐  ┌─────────────────┐ │
│  │  AI Avatar     │  │  LLM         │  │  Speech-to-Text │ │
│  │  Engine        │  │  Processing  │  │  & TTS Engine   │ │
│  └────────────────┘  └──────────────┘  └─────────────────┘ │
└─────────────────────────────────────────────────────────────┘
```

### Communication Flow

```
User Input → Frontend → Backend → LiveAvatar API
                ↓
          LiveKit Room
                ↓
      Video/Audio Stream → Frontend Display
```

---
### System Architecture

    ### Sequence Diagram : Session Creation and Text Chat

<p align="center">
  <img src="https://uml.planttext.com/plantuml/svg/RLGzRzj03Dq5w3yGNZ8PtZqKYPqKTTK0HcIWGz61aHZxKEbEkACS6qN_UtaVagMcWmr-wP7laTAzOxJSjqsUiUA6eBmwfXQsfksC9itmgF1eiSspFEkm-eL7WiLdQpIJhk6XwnfL8IkZ5_0xpm1-l11Mx1C_0Hq4JvoGUZYZTDkUa6_ueIecOir-1zj6ZPdzBeI_gJCLYg5yB48y-UBwjFyDdM2v_3G1Z5OCHgn9P8hoPyPm8uOdM98zansuFLqwIywbQ1WaXKAw54EK47AQhMcQL79pHoff1e-ZAWfLoHxe3Atyc7E0cnUIutDp0ayN9gkn6V9ku31fBuACOiRGltBlz9j5nxQlkBSqLJwK5TgyDrHBlmswc2usQP9Qy5ub2ej1bfADbTc6GNPw-KojiLTunYv940fTGhZpL3LL76F-CZpXfCmQlXmE-vN_A_FijidfOjVmdLvB8wlabLWlXssU9Jt6if5u11Ii3mB7gTPW2UlLkrLCiU7uQAWhDcle7Rd_vSPvMjGYWVFqj642guud1lCsbLKkkLcoQWcmhvLPdLLDnYTa4OIjqaTGixtacJzLZ_SHr-yZtWmgxU0hQdd7MyMdkt2p7Lbdv4mKNm45fF8lzeNdYFVYo2VYBm00" alt="Logo" width="100%"/>
</p>

### Sequence Diagram :  Voice Interaction

<p align="center">
  <img src="https://uml.planttext.com/plantuml/svg/pLPDZzem4Br7odyOSLYnQg5t95RBxXPrLLP5iDqJ5nEFm2BOaUr0gwh_lMCxX2IRPAyzGSoRZ_VcZSEziKpR_9Z6aHKsHNXJ8a5ubXOrIwnG4kQfEiTH7D6Zql3Je8wZZ8948Z8cBGnMI3_1N2iAadm0p9GF3UI3LcUAXnVaWZtXYKePZ_S73V12dF2xiB16VKBjOSLH2t1sOaG4Pild4XYENEVJAJnIFqBcAZS5mnV54QRJE7A4O7HNjZo1nrGa1nXybMnR2kBWWpYwW5o0xta2ExGkXNyQ_c4v5se2LkVuzzPh9gWDl13q7p2gbVDdQwkH7UE8OpEaNhHGO09Plas5sR_Ib0v3NzL__RoHHkKwGSeh4gsolP9ORQIKy29llHcV19OXEV9wSSTp0kkzEZlH3HqBkHkFnmCGaek4aJyAkODe93fDpZ1lewhMXNJh3Dc1Ogs2OzbiALA5R507F4tWDDPA-tULOKzWhlIPQLv0JQ5gZVtL5nNZDD9GPvZiHrQDNl6NxKCkjI8J6pWBkuV5ugKFwtAvd25xiuCgOHg3D8aMcPVkqqRE79ylRuAZ0eqcKz9WpItlcRKCb-eNMcxaq5Pht7R5L0ktcBIqKzqfr_WdORAK_OPBjIroE99WR8TjvbewB0kAN7bwJorp4oR2qaFV-YwrcySDV5CfTxw2RMwjal_1ybx3rkxM3Q0L9afpTwbshLf0jAxQU_OhJ94Px2HUxK5bVIrKBaIYHvp2JZsaQjjvAwtTGS2LG-wvUjfNoSTtB6tFSfK6ezaNgReNRFNH3dLiGzEP7wz2cEHb3Mx0VpIiJRystZNzhwOAxiTyFkWOHYvhBudQ-w1b5xmVmkoi2p1jF4BbewlCGzFSSRWd4Fs9-0S0" alt="Logo" width="100%"/>
</p
  
### Class Diagram : 

<p align="center">
  <img src="https://uml.planttext.com/plantuml/svg/lLRVJzim47wlrF_1ucKmMj1U8uG8fKWLC50RqAPfGcvoW8TZPxRJWIR-zvtpWzZvKV6qbxJoVJdVVVVTNKwqeShaAH-F33CSIBWWuORY8PazKKDMhzf0IgPangdMv8pHHqNJyMWyocZyJ1-1x9mhAGo8P8Vy7Oy8YGjWwQDmKPmIT962rlY63iXL-U_7pzh4H9QRW6YZc7XyFzGpAGJ41fA0hANaG4LZkvGqGN2FPGcnL0EsEybYk989p0LTynx76vQ0NC93GF1nlVw5rzSccYTimAIaJ7tBqHAFZflK4qRBk43rk-0ofZoqLqGAgUq3bSzzKjIiP7XtBo0tIgPCmz56ikIunZnHaN1OOLq68L1GyCx884uRcNaeQ_LYUMTygmyFvVf8c8xBIlkMANcGAgKcOYdi9jJ0NbiYEbQIyqYUIcDawhxzPZLQgx7IMor530Tv0ULxsoS6Napd3E_67DCi86SOGNty3Aykqhijl5dCE0DXcljY1VZo2iDWKhWaLKTBq9aK6fpQ93LQbx-Bf8zRx-AMCoVTF8xHrXAxfQ5otSwwCaJo6KJRnja6dfcvLNp0qdaBWtppHiOf_cbF33ihiD-DBIYePchGsA3RAZKxEsXsLBgUr0aln8CyxccHca45loT4WHvkXEGZq3wkxTMkh8PfAoMGXAWmaQThK1sNbvXdsTKhK1lijuQ4oyNTFBmBet1vVngkvkqsSCmellkB-VSsucn-7jvUHlSbQiXwTxsOTPpFhhz6ys_H_UBCj_Y9kS4FgHmRY7eJeVkIiTHzb7phhqF-Vn1p4yZy9KEnw33BcZXkhbSHEQmkFIpPwRUXxdhRO_vYG0dAIQK3xJLAGnhMkdtjvaljNHyMN0wRYnRPPfPPhqGlcB6xpHbkrUpE5P-GmG9k6_Jx9ClNdEcdOlNj6liSyf6BNgotav3O26VvRlN5CI4oCpQf8PyeFDZWm9vKQrCDBP8B8V_WLyCZd59tlhAEvWHDeNsMuTMPwHkCdt3JSrg4-CGoFHuvdq_JwN6pKGAIOu4wTgSi0Kcfi5zP7kZpT5elmS3Mor0cBE9zKralhVKHu1mqkRAuySWHkeNwmngHCZUWiVZZKMkEr-5vWwrEeuMrKJfprKcbEngTWEqOy8BT6WBcZ1HGpWVTzcEtKLw9kYJ0TMixrA8ztTJPjzVrmK4hfPGf9LMHqWbA6h_I_m40" alt="Logo" width="100%"/>
</p>

### Component Diagram : 

<p align="center">
  <img src="https://uml.planttext.com/plantuml/svg/RLGzRzj03Dq5w3yGNZ8PtZqKYPqKTTK0HcIWGz61aHZxKEbEkACS6qN_UtaVagMcWmr-wP7laTAzOxJSjqsUiUA6eBmwfXQsfksC9itmgF1eiSspFEkm-eL7WiLdQpIJhk6XwnfL8IkZ5_0xpm1-l11Mx1C_0Hq4JvoGUZYZTDkUa6_ueIecOir-1zj6ZPdzBeI_gJCLYg5yB48y-UBwjFyDdM2v_3G1Z5OCHgn9P8hoPyPm8uOdM98zansuFLqwIywbQ1WaXKAw54EK47AQhMcQL79pHoff1e-ZAWfLoHxe3Atyc7E0cnUIutDp0ayN9gkn6V9ku31fBuACOiRGltBlz9j5nxQlkBSqLJwK5TgyDrHBlmswc2usQP9Qy5ub2ej1bfADbTc6GNPw-KojiLTunYv940fTGhZpL3LL76F-CZpXfCmQlXmE-vN_A_FijidfOjVmdLvB8wlabLWlXssU9Jt6if5u11Ii3mB7gTPW2UlLkrLCiU7uQAWhDcle7Rd_vSPvMjGYWVFqj642guud1lCsbLKkkLcoQWcmhvLPdLLDnYTa4OIjqaTGixtacJzLZ_SHr-yZtWmgxU0hQdd7MyMdkt2p7Lbdv4mKNm45fF8lzeNdYFVYo2VYBm00" alt="Logo" width="100%"/>
</p>

 ### Object Diagram 

<p align="center">
  <img src="https://uml.planttext.com/plantuml/svg/fLJRZjCm47slb7yO-h8I8jcahRPGQPSj1K4hgaNjQYKU7MUQcYPsP3kz2F7ls4wo9Dtb8f6tEJEUSp9dx5kbYTHbddazpNI6CAMQxH7Mg1GJ7DQQQ0GVxk9lI3MyPoIL9FTwNazKI7-w9wR5R4iqpBdfnYdsWIYW5ldkzG2OcWdEJJ4cS0rQbbYX3u9HN8e4Ft0IPowv8PcgiokaGYQCfrtuio1Ty4TRp4g8l2j3MiJ9KEvNhg5F6pLz2vSoi-11gSdbvHPFANB_U3m6cHd3Zkc0PgAqbHsUfHaFIH4Ynv6hDAeva2SeRR-ledJjDHwrZJ_X2HQ4uolOYiE5WeEGkxTL1SlHQCiBKpO81rT-6Fc32ABHP1XEmj2MxCnXqwDKAFreF1oFhiQZq7w_qpLeT0tETLLsTQHzaQZr2L8XaXUmA9M6WoH5OQTS5a4G_8FAOKibSGo_T0wVqTcirvnlX9EgQg1MwuAvtOZ-A4f8ZBZnNszmrAYfA-x53hajmjDY6t-ax8ujcX8gqVYTJEqlrbg6R-pCpgGyi0G5t4j2Tqx9tiLEnuvn9y515Qye9RLBvEg3jGk36SbH4fl7nqskrhp3D2qJrcOYBkumEUWFJ4j6fIYsWkDVsTwPOyRrnvky94LxqYQig9yEsFHh733sFE_SkN4sxfZtFzPSm0epeaqNjMM5ydhkBV7z6tUR9v0JRfQymL_wlhk1tN3GEbLBcfWdG4XxpZqAjj0vQ_0oLbIo61LeqKexEvwaMnEqHPrPDNiS13Vjn0JCOsQe2y6JgedNkpNkc8Vt9m00" alt="Logo" width="100%"/>
</p>

 ### Application state Diagram 

<p align="center">
  <img src="https://uml.planttext.com/plantuml/svg/ZLJ1Rjim3BqBq3yGEHRe3_WmD6WpRC0254cw7OOT58b9X2gI8Sh1-lUZ53jn71lToR3utXCVIV69aegfEJefaaqEOLxNpcgLRF2mJYeXB9K-M8zIIF7xuGyyFdw1xyQL__mj1y_1UzJ9-dq5RuGHD8ky4ypMMJw7JnYfgCwakABxP3GLh94etwmZyjK6gD6QZtQDSnztl4MC8LQNkvcsKzQXaQ94BfcsAKLCqIBbl2yt5im6_wRdWqehLEQZWXVSgSObE0Q3G-ZFO3KkET1Y5rvjkGIdVDmIfBZHAxJN6B8DJZp7sdm8lI58V235BQ1mVYcRdNuDSOLK1q_iOyaOjSTCPT8zOipE_AIu1-m-GqonV-kYa7vOIkXPZVsoQ1CQgivkYorGNE0Jknl13HmMKcUnHlLEVNjdoIb_yyRO0FKPdHivON4qspkZKxaEc_XYwR-wk48Tec6zryscWc_16JXQ3TicfU2bw8V7Qx92XuejT8oniWowTuM03iVQOPf8ZategKUuy6OsslNFILCr_9mfnGsczngxHyxpdtiiXG-yPgBT7nA4tNKTI05TKq_MO01Al1QE-TXIEv6WlE4esMtUIAm8MUnUT53gddGtRQoOfoz7ikOUFKRUGTGE50tad_Y7r-O_" alt="Logo" width="100%"/>
</p>


## Technology Stack

### Frontend
- **React** (v18+) - UI framework
- **LiveKit Client SDK** - Real-time audio/video streaming
- **JavaScript (ES6+)** - Programming language
- **CSS3** - Styling with animations
- **Vite** - Build tool and dev server

### Backend
- **Node.js** (v18+) - Runtime environment
- **Express.js** - Web framework
- **Axios** - HTTP client
- **dotenv** - Environment variable management
- **CORS** - Cross-origin resource sharing

### External Services
- **LiveAvatar API** - AI avatar platform
- **LiveKit** - WebRTC infrastructure
- **Knowledge Base** - Context for AI responses

---

## System Components

### 1. Frontend Components

#### AvatarChat Component
**Location:** `client/src/components/AvatarChat.jsx`

**Responsibilities:**
- Manage LiveKit room connection
- Handle user inputs (text and voice)
- Display video stream and chat messages
- Coordinate voice recording and streaming
- Manage UI state

**Key State Variables:**
```javascript
- messages: Array         // Chat history
- isConnected: Boolean    // Connection status
- isRecording: Boolean    // Voice recording state
- isVoiceModeEnabled: Boolean  // Continuous voice mode
- isLoading: Boolean      // Request state
- isAvatarSpeaking: Boolean    // Avatar response state
```

#### API Utilities
**Location:** `client/src/utils/api.js`

**Functions:**
- `createSession()` - Initialize avatar session
- `endSession(sessionId)` - Terminate session

### 2. Backend Components

#### Session Controller
**Location:** `server/controllers/chatController.js`

**Endpoints:**
- `POST /session/create` - Create new avatar session
- `POST /session/end` - End active session

**Functions:**
- `startSession(req, res)` - Create and start LiveAvatar session
- `endSession(req, res)` - Stop session and cleanup

#### LiveAvatar Service
**Location:** `server/services/liveAvatarService.js`

**Functions:**
- `createLiveAvatarSession()` - Create session token and start session
- `stopLiveAvatarSession(sessionToken)` - Stop active session

**Configuration:**
```javascript
- Avatar ID: 998e5637-cfca-4700-891e-8a40ce33f562
- Voice ID: Configurable (uses avatar default if not set)
- Mode: FULL (AI-powered conversation)
- Context ID: Knowledge base for personality
```

### 3. Configuration Files

#### Environment Variables (.env)
```env
# LiveAvatar Configuration
LIVEAVATAR_API_KEY=your_api_key_here
CONTEXT_ID=your_context_id_here
AVATAR_ID=998e5637-cfca-4700-891e-8a40ce33f562
VOICE_ID=optional_voice_id

# Server Configuration
PORT=5000
```

---

## Setup Guide

### Prerequisites
- Node.js 18+ installed
- npm or yarn package manager
- LiveAvatar API account
- Modern web browser with microphone access

### Installation Steps

#### 1. Clone Repository
```bash
git clone <repository-url>
cd ai-avatar-chat
```

#### 2. Backend Setup
```bash
cd server
npm install
```

#### 3. Frontend Setup
```bash
cd client
npm install
```

#### 4. Create Knowledge Base
```bash
cd server
node createContext.js
```

Copy the generated `CONTEXT_ID` to your `.env` file.

#### 5. Configure Environment Variables
Create `server/.env`:
```env
LIVEAVATAR_API_KEY=your_liveavatar_api_key
CONTEXT_ID=your_context_id_from_step_4
AVATAR_ID=998e5637-cfca-4700-891e-8a40ce33f562
PORT=5000
```

#### 6. Start Services

**Terminal 1 - Backend:**
```bash
cd server
npm start
```

**Terminal 2 - Frontend:**
```bash
cd client
npm run dev
```

#### 7. Access Application
Open browser and navigate to: `http://localhost:5173`

---

## API Documentation

### Backend Endpoints

#### 1. Create Session

**Endpoint:** `POST /session/create`

**Description:** Creates a new LiveAvatar session and returns connection credentials.

**Request:**
```http
POST /session/create
Content-Type: application/json
```

**Response:**
```json
{
  "success": true,
  "sessionId": "uuid-string",
  "sessionToken": "jwt-token-string",
  "livekitUrl": "wss://livekit-server-url",
  "livekitToken": "livekit-jwt-token"
}
```

**Error Response:**
```json
{
  "error": "Failed to create session",
  "details": "Error message"
}
```

**Status Codes:**
- `200` - Success
- `500` - Server error

#### 2. End Session

**Endpoint:** `POST /session/end`

**Description:** Terminates an active LiveAvatar session.

**Request:**
```http
POST /session/end
Content-Type: application/json

{
  "sessionId": "uuid-string"
}
```

**Response:**
```json
{
  "success": true,
  "message": "Session ended"
}
```

**Error Response:**
```json
{
  "error": "Session not found"
}
```

**Status Codes:**
- `200` - Success
- `404` - Session not found
- `500` - Server error

### LiveAvatar API Integration

#### 1. Create Session Token

**Endpoint:** `POST https://api.liveavatar.com/v1/sessions/token`

**Headers:**
```
X-API-KEY: your_api_key
Content-Type: application/json
```

**Request Body:**
```json
{
  "mode": "FULL",
  "avatar_id": "avatar-uuid",
  "avatar_persona": {
    "voice_id": "voice-uuid",
    "context_id": "context-uuid",
    "language": "en"
  }
}
```

**Response:**
```json
{
  "session_id": "uuid",
  "session_token": "jwt-token"
}
```

#### 2. Start Session

**Endpoint:** `POST https://api.liveavatar.com/v1/sessions/start`

**Headers:**
```
Authorization: Bearer {session_token}
Content-Type: application/json
```

**Response:**
```json
{
  "livekit_url": "wss://...",
  "livekit_client_token": "jwt-token"
}
```

#### 3. Stop Session

**Endpoint:** `POST https://api.liveavatar.com/v1/sessions/stop`

**Headers:**
```
Authorization: Bearer {session_token}
Content-Type: application/json
```

---

## Features

### 1. Text Chat
- Real-time messaging with AI avatar
- Message history with timestamps
- Typing indicators
- Auto-scroll to latest message
- Message sent confirmation

### 2. Voice Interaction

#### Continuous Voice Mode
- Always-on microphone
- Real-time speech-to-text
- Natural conversation flow
- Visual indicator when listening
- One-click enable/disable

#### Push-to-Talk
- Hold button to record
- Release to send
- Visual recording feedback
- Recording status indicator
- Works alongside text input

### 3. Avatar Features
- Real-time lip-sync
- High-quality video streaming
- Natural voice synthesis
- Contextual responses based on knowledge base
- Expressive gestures and emotions

### 4. User Interface
- Clean, modern design
- Responsive layout
- Loading states and indicators
- Error handling with user feedback
- Accessible controls

---

## Technical Details

### LiveKit Integration

#### Connection Management
```javascript
// Connect to LiveKit room
const room = new Room();
await room.connect(livekitUrl, livekitToken, {
  autoSubscribe: true
});

// Subscribe to tracks
room.on(RoomEvent.TrackSubscribed, (track) => {
  if (track.kind === Track.Kind.Video) {
    videoElement.srcObject = track.attach().srcObject;
  }
});
```

#### Text Messaging
```javascript
// Send text to avatar
await room.localParticipant.sendText(message, {
  topic: 'lk.chat'
});

// Receive transcriptions
room.registerTextStreamHandler('lk.transcription', async (reader) => {
  const message = await reader.readAll();
  const isFinal = reader.info.attributes['lk.transcription_final'] === 'true';
  // Process transcription
});
```

#### Voice Streaming
```javascript
// Publish audio track
const stream = await navigator.mediaDevices.getUserMedia({ 
  audio: {
    echoCancellation: true,
    noiseSuppression: true,
    autoGainControl: true
  } 
});

await room.localParticipant.publishTrack(audioTrack, {
  source: Track.Source.Microphone
});
```

### Knowledge Base Configuration

The knowledge base defines Jane Smith's personality:

```javascript
{
  name: "Jane Smith - Water Cooler Chat",
  prompt: `You are Jane Smith, a friendly colleague having casual 
  water cooler conversations. Keep responses SHORT (1-2 sentences).
  Be natural and conversational. Reference office situations like 
  meetings, deadlines, and projects. Show genuine interest and 
  occasionally ask follow-up questions.`
}
```

### Session Management

Sessions are stored in-memory on the backend:

```javascript
const activeSessions = new Map();

// Store session
activeSessions.set(sessionId, {
  sessionToken,
  createdAt: Date.now()
});

// Retrieve session
const session = activeSessions.get(sessionId);

// Cleanup
activeSessions.delete(sessionId);
```

---

## Troubleshooting

### Common Issues

#### 1. "No credits available"
**Problem:** LiveAvatar account has run out of credits.

**Solution:**
- Check your LiveAvatar account balance at https://app.liveavatar.com/developers
- Purchase additional credits or wait for free tier reset
- Verify your subscription status

#### 2. "Voice not found"
**Problem:** Specified voice ID doesn't exist or isn't compatible.

**Solution:**
- Run `node listVoices.js` to see available voices
- Update `VOICE_ID` in `.env` or remove it to use avatar's default voice
- Ensure voice supports the selected language

#### 3. Microphone not working
**Problem:** Browser doesn't have microphone permission.

**Solution:**
- Check browser permissions (usually a camera icon in address bar)
- Ensure HTTPS connection (required for microphone access)
- Try a different browser (Chrome/Edge recommended)
- Check OS-level microphone permissions

#### 4. Avatar not responding
**Problem:** Messages sent but no avatar response.

**Solution:**
- Check network connection
- Verify LiveKit connection is active (check console logs)
- Ensure session hasn't expired
- Check backend logs for errors
- Restart the session

#### 5. Video not displaying
**Problem:** Avatar video stream not showing.

**Solution:**
- Check browser console for errors
- Verify LiveKit connection
- Ensure video element has correct srcObject
- Check if tracks are being subscribed properly
- Clear browser cache and reload

#### 6. Session creation fails
**Problem:** Backend returns error when creating session.

**Solution:**
- Verify `.env` configuration:
  - `LIVEAVATAR_API_KEY` is valid
  - `CONTEXT_ID` exists
  - `AVATAR_ID` is correct
- Check backend console for detailed errors
- Ensure LiveAvatar API is accessible
- Verify account has active subscription

### Debug Mode

Enable detailed logging:

**Frontend:**
```javascript
// In AvatarChat.jsx
console.log("Room state:", roomRef.current?.state);
console.log("Tracks:", roomRef.current?.localParticipant.tracks);
```

**Backend:**
```javascript
// In liveAvatarService.js
console.log("Request:", requestBody);
console.log("Response:", response.data);
```

### Performance Optimization

#### Reduce Latency
- Use wired internet connection
- Close unnecessary browser tabs
- Ensure sufficient CPU/memory available
- Use modern browser (latest Chrome/Edge)

#### Improve Video Quality
- Stable internet connection (10+ Mbps recommended)
- Reduce background network usage
- Check WebRTC stats in browser DevTools

---

## File Structure

```
project-root/
│
├── server/
│   ├── controllers/
│   │   └── chatController.js       # Session management endpoints
│   │
│   ├── services/
│   │   └── liveAvatarService.js    # LiveAvatar API integration
│   │
│   ├── .env                         # Environment variables
│   ├── server.js                    # Express app entry point
│   ├── createContext.js             # Knowledge base creation script
│   ├── listVoices.js               # Voice listing utility
│   └── package.json
│
├── client/
│   ├── src/
│   │   ├── components/
│   │   │   ├── AvatarChat.jsx      # Main chat component
│   │   │   └── AvatarChat.css      # Component styles
│   │   │
│   │   ├── utils/
│   │   │   └── api.js              # API client functions
│   │   │
│   │   ├── App.jsx                 # Root component
│   │   └── main.jsx                # Entry point
│   │
│   ├── public/
│   ├── package.json
│   └── vite.config.js
│
└── README.md
```

---

## Environment Variables Reference

### Server (.env)

| Variable | Required | Description | Example |
|----------|----------|-------------|---------|
| `LIVEAVATAR_API_KEY` | Yes | API key from LiveAvatar | `abc123...` |
| `CONTEXT_ID` | Yes | Knowledge base ID | `uuid-string` |
| `AVATAR_ID` | No | Specific avatar ID | `998e5637...` |
| `VOICE_ID` | No | Custom voice ID | `f7c46f14...` |
| `PORT` | No | Server port | `5000` |

---

## Best Practices

### Security
1. Never commit `.env` files
2. Use environment-specific API keys
3. Implement rate limiting in production
4. Validate all user inputs
5. Use HTTPS in production

### Performance
1. Implement session cleanup for inactive sessions
2. Use connection pooling for API requests
3. Implement proper error boundaries
4. Optimize bundle size
5. Use lazy loading where appropriate

### Code Quality
1. Follow ESLint rules
2. Write meaningful comments
3. Use TypeScript for type safety (optional enhancement)
4. Implement proper error handling
5. Write unit tests for critical functions

---

## Future Enhancements

### Potential Features
1. **Multi-language Support** - Support for languages other than English
2. **Custom Avatars** - Allow users to select different avatars
3. **Conversation History** - Persist chat history across sessions
4. **Screen Sharing** - Share screen during conversation
5. **Group Conversations** - Multiple users chatting with avatar
6. **Sentiment Analysis** - Detect user emotions and adjust responses
7. **Voice Cloning** - Use custom voice models
8. **Mobile App** - Native iOS/Android applications
9. **Analytics Dashboard** - Track usage and conversation metrics
10. **WebRTC Recording** - Record conversations for playback

### Technical Improvements
1. Migrate to TypeScript
2. Add comprehensive unit and integration tests
3. Implement Redis for session management
4. Add database for conversation persistence
5. Implement CI/CD pipeline
6. Add monitoring and logging (e.g., Sentry)
7. Implement caching strategy
8. Add load balancing for scale
9. Implement WebSocket fallback
10. Add progressive web app (PWA) features

---

## Credits

### Technologies Used
- **LiveAvatar** - AI avatar platform
- **LiveKit** - Real-time communication infrastructure
- **React** - Frontend framework
- **Express.js** - Backend framework
- **Node.js** - Runtime environment

### Documentation
- LiveAvatar API Documentation: https://docs.liveavatar.com
- LiveKit Documentation:
