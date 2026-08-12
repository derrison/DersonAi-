# DersonAI

A single-page text-to-video generator UI built on the [Runway API](https://dev.runwayml.com).

Type a prompt, pick a model / aspect ratio / duration, hit **Action — Generate**, and watch the render land in the playback monitor. Every clip you generate in a session lines up in the "takes" reel below.

## Getting started

1. Get a Runway API key at [dev.runwayml.com](https://dev.runwayml.com).
2. Open `index.html` in a browser (or serve it — see below).
3. Paste your API key into the **Credentials** field. It's kept only in the page's memory: nothing is saved to disk or sent anywhere but Runway's API.
4. Write a prompt, choose your settings, and generate.

You can just double-click `index.html` to open it locally, or serve it:

```bash
npx serve .
# or
python3 -m http.server 8000
```

## A note on CORS

Runway's API (`api.dev.runwayml.com`) is designed to be called from a server, not directly from a browser tab. Depending on Runway's current CORS policy, calls made straight from this page may be blocked by the browser. If every generation fails immediately with a network error, that's what's happening — the fix is a small backend proxy that holds the API key server-side and forwards requests to Runway on the page's behalf. This repo ships only the client; adding that proxy is a natural next step if you hit the wall.

## What it calls

- `POST /v1/text_to_video` — submits the generation job
- `GET /v1/tasks/{id}` — polled every 5s until the job succeeds or fails

Models supported: `veo3.1`, `veo3.1_fast`, `veo3`. Durations: 4 / 6 / 8 seconds (Runway's text-to-video limits). Ratios: 1280:720, 720:1280, 1104:832, 832:1104, 960:960, 1584:672.

## License

MIT — see `LICENSE`.
