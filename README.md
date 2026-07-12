# 🎙️ Supertonic 3 — TTS & Audiobook Studio

A no-code Google Colab notebook that turns [Supertonic 3](https://github.com/supertone-inc/supertonic) — Supertone Inc.'s fast, open-weight, on-device multilingual text-to-speech model — into a full production studio: audiobooks, podcasts, dialogue scenes, a live API server, and more. Everything is driven by point-and-click forms. **No code editing required.**

> This is an independent, unofficial notebook built around the open-weight Supertonic 3 model. It is not affiliated with or endorsed by Supertone Inc. See [Licensing](#-licensing--attribution) below before using it commercially.

---

## ✨ What's inside

| # | Cell | What it does |
|---|------|---------------|
| 1 | 🔧 Setup | Installs everything and loads the model. Run once per session. |
| 2 | 🎙️ Quick Text-to-Speech | Type text, pick a voice/language, generate a clip. |
| 3 | 🧬 Custom Voice Upload | Bring your own voice via Supertone's free Voice Builder, or train one from a longer recording with an [independent tool](https://github.com/Fawzan09/voice-builder-for-supertonic-3). |
| 4 | 🔊 Preview All Voices | Hear a sample of every built-in voice before committing to one. |
| 5 | 🧪 Voice Blender *(experimental)* | Mix two voices together at any ratio to create a new hybrid voice. |
| 6 | 🧹 Text Cleanup | Strips page numbers, repeated headers/footers, and broken line-wraps from messy PDF/scanned text. |
| 7 | 📚 Audiobook Generator | Upload a `.txt` / `.epub` / `.pdf`, get back fully narrated, chapter-split audio with subtitles. |
| 8 | 📱 M4B Export | Packages chapters into a real `.m4b` with chapter markers, metadata, and cover art — playable in Apple Books, Audiobookshelf, Plex, etc. |
| 9 | 🎭 Multi-Voice Dialogue | Script out a scene as `VoiceName: line` and get a fully cast reading. |
| 10 | 📂 Batch Convert | Turn a folder of `.txt` files into narrated audio in one pass. |
| 11 | 🎚️ Audio Mastering | Loudness-normalize output to Audiobook/Podcast/Broadcast targets, with silence trimming. |
| 12 | 🎵 Intro/Outro Music Mixer | Crossfade narration with intro/outro music beds. |
| 13 | 🌐 Voice AI API Server | Runs Supertonic as a live HTTP API (native + OpenAI-compatible endpoints), optionally with a public URL. |
| 14 | 📡 Podcast RSS Feed Generator | Turns your episodes into a real, spec-compliant Apple Podcasts/Spotify feed, with a live test preview. |
| 15 | 🛑 Stop All Background Servers | Cleanly shuts down anything started by Cells 13/14. |
| 16 | 💾 Save to Google Drive | Backs up everything you've generated. |

---

## 🚀 Getting started

1. Open the notebook in [Google Colab](https://colab.research.google.com) (upload the `.ipynb`, or open it directly if hosted on Drive/GitHub).
2. Run **Cell 1 (Setup)** first. This installs dependencies and downloads the model (~400MB, one-time per session).
3. Every other cell is a form — fill in the fields on the right of the cell and press ▶️. You never need to open or read the underlying code.
4. Generated files land in `/content/supertonic_output` inside your Colab session and are offered as downloads automatically.

**Requirements:** just a free Google account. No GPU needed — Supertonic 3 is designed to run on CPU. A free-tier Colab runtime is enough for most use; a paid Colab tier will simply run faster for long audiobook jobs.

---

## 🌟 Want a custom voice that actually sounds like you (or your character)?

The built-in voices (M1–M5, F1–F5) are great out of the box, but Cell 3 also plugs into **[Custom Voice Style Trainer for Supertonic 3](https://github.com/Fawzan09/voice-builder-for-supertonic-3)** — a companion Colab notebook that trains a voice style from a **1–3 minute reference recording** instead of a quick 30-second sample, for a noticeably closer match.

- 🎯 Trains on your own free Colab GPU — no ongoing API costs
- 🌍 Test the trained voice across English, Hindi, Arabic, Japanese, and Korean
- 💰 **One-time purchase, unlimited voices** — train as many as you want, forever, no subscription
- 🔓 Outputs a standard `.json` voice style that drops straight into Cell 3 of this notebook

**Get it here → https://buymeacoffee.com/fawzan/e/554254**

*(This is a separate, independent tool — not made by Supertone Inc. — so it's an optional add-on to this notebook, not a requirement. See its repo for full details, limitations, and responsible-use terms.)*

---

## 🧭 A few things worth knowing before you dive in

- **Colab resets its Python state on disconnect/idle-timeout.** If any cell throws a `NameError` about something not being defined, the fix is almost always: re-run **Cell 1**.
- **Custom voices aren't cloned from raw audio by default.** Supertonic 3's open-weight package doesn't include a voice-cloning pipeline out of the box — see the callout above, or use [Supertone's free Voice Builder](https://supertonic.supertone.ai/voice-builder) for a quick 30-second option.
- **The Voice AI API Server and Podcast RSS preview are session-bound.** Any public URL they generate (via a free Cloudflare tunnel) only works while your Colab session stays open — great for testing, not for permanent production use. See each cell's notes for what to do instead.
- **Re-running Cells 13/14 is safe.** They automatically clean up any server left running from a previous run in the same session, so you don't need to manually stop things first.
- **Cover art for the podcast feed** should be square, 1400×1400 to 3000×3000 px, JPG or PNG — the cell will warn you if it isn't, but won't block you.

---

## 🛠️ Troubleshooting

| Symptom | Likely cause / fix |
|---|---|
| `NameError: name 'tts' is not defined` (or similar) | Setup wasn't run this session — run Cell 1, then retry. |
| `OSError: Address already in use` on Cells 13/14 | Fixed as of this version — both cells now clean up prior runs automatically. If you still see it, re-run the cell once more. |
| Audiobook chapter comes out silent or tiny | Usually PDF-extraction garbage characters or an oversized run-on sentence in the source text. Try running Cell 6 (Text Cleanup) on the source first. |
| M4B file plays in some apps but not others | Make sure you're on the latest version of this notebook — it uses `-movflags +faststart` so strict player apps can open the file correctly. |
| Cover art embedding fails on M4B export | The notebook falls back to shipping the audiobook without a cover and tells you why, rather than producing a broken file. |
| Podcast feed URL "doesn't work" in Apple/Spotify | The live preview URL is temporary by design — see the hosting notes printed after Cell 14 for how to publish permanently. |

---

## 📜 Licensing & attribution

This notebook is built on the **open-weight Supertonic 3** model and reference tooling published by **Supertone Inc.**

- **Supertonic's reference/inference code** is released under the **MIT License**.
- **Supertonic 3's model weights** are released under the **OpenRAIL-M License** — open and commercially usable, but with *use-based restrictions*: no harmful use, no non-consensual voice impersonation, and an attribution requirement. Read the full terms before commercial use: https://huggingface.co/Supertone/supertonic-3/blob/main/LICENSE
- **Voice Builder** (used for custom voices) is a free tool provided by Supertone Inc. at https://supertonic.supertone.ai/voice-builder
- The **[Custom Voice Style Trainer for Supertonic 3](https://github.com/Fawzan09/voice-builder-for-supertonic-3)** is a separate, independent, paid tool for training a voice style from a longer reference recording — it is not made or endorsed by Supertone Inc., and using it is entirely optional. Its own repository documents its licensing, limitations, and OpenRAIL-M responsible-use obligations in detail.
- The **Voice Blender** feature (Cell 5) is an experimental technique built for this notebook, interpolating voice-style data directly — it is not an official Supertone feature and isn't guaranteed to work for every voice pair.

Note that this notebook (the workflow, forms, and code wrapping the model) is a separate work from the underlying Supertonic model itself, which remains Supertone Inc.'s work under its own license above. Any audio you generate with this notebook is subject to the OpenRAIL-M terms — particularly around consent for voice likeness and prohibited uses.

---


## Notebool : (https://buymeacoffee.com/fawzan/e/556321)

---

## 🔒 Terms of use for buyers

Purchasing access to this notebook gives you a **personal-use license to use it** — it does not give you the right to resell, redistribute, or repackage it.

- ✅ You may use this notebook for your own personal or commercial projects — audiobooks, podcasts, voiceovers, client work, etc.
- ✅ You may sell or distribute the **audio you generate** with it, subject to the OpenRAIL-M terms above (consent for any voice likeness used, no prohibited uses).
- ❌ You may **not** resell, redistribute, share, or re-license this notebook — or any copy or derivative of it — to any other person or party.
- ❌ You may **not** repackage or relabel this notebook as your own product for sale.

This notebook is licensed to you for use, not resale. It remains the property of **[Your Name / Brand]** and is provided as-is, with no warranty.

*(This is a plain-language summary, not a substitute for a formal license agreement. If you want these terms to be legally binding — e.g. for a storefront like Gumroad — consider having a lawyer turn this into a proper EULA, and check whether your sales platform has its own terms that apply on top of this.)*

---

## ⚠️ Limitations

- CPU-based inference means long audiobooks (multi-hour books) will take real wall-clock time to generate — budget accordingly.
- The Voice Blender is experimental and not guaranteed to produce good results for every voice combination.
- Public URLs from the API Server and Podcast preview are unauthenticated — don't share them publicly, and stop them (Cell 15) when you're done.
- This notebook does not perform real-time/streaming synthesis — it's built for batch generation (files in, files out), not live conversational use.

---

## 🙏 Credits

Built on [Supertonic 3](https://github.com/supertone-inc/supertonic) by Supertone Inc. Not an official Supertone product.
