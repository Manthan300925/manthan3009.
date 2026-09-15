# ABGI Cinematic AI Receptionist

Cinematic ABGI website with a Retell AI browser voice receptionist.

## Retell integration

This version uses Retell's current `RetellClient` Web Call architecture. The browser SDK handles the WebRTC/LiveKit media connection, while the Express server keeps `RETELL_API_KEY` private and creates the short-lived web-call session.

The browser does **not** contain the Retell API key.

## Local setup

Requirements: Node.js 20+ (Node.js 22+ recommended).

1. Extract the ZIP.
2. Copy `.env.example` to `.env`.
3. Put your Retell secret API key in `.env`:

```env
RETELL_API_KEY=key_your_real_retell_secret
RETELL_AGENT_ID=agent_480f5243f2aa6b7ebf452f5fe1
```

4. Install dependencies:

```bash
npm install
```

5. Start the website and backend:

```bash
npm run dev
```

6. Open `http://localhost:5173`.
7. Click **Talk to AI** → **Start Voice Call**.
8. Allow microphone access if Chrome asks.

## Important

Do not paste the Retell API key into React/Vite code and do not commit `.env`.

For Render, deploy the project as a Node web service and add `RETELL_API_KEY` and `RETELL_AGENT_ID` under Environment Variables. Render should serve the production site over HTTPS so browser microphone/WebRTC access is allowed.

## Troubleshooting

- `GET /api/health` should report `retellConfigured: true`.
- If the browser reports a WebRTC/microphone problem, make sure the deployed site is HTTPS and Chrome has microphone permission for the site.
- The current frontend surfaces the actual Retell SDK error instead of the old generic `Error starting call` message.
