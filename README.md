# SOULSPACE

An all-emotion AI companion in a single web page. It listens to what you write, reads a mix of feelings (not just one), and answers the way a good friend would for that feeling. A glowing **Emotion Spectrum Orb** and **live mood music** follow along.

The page is one file, `index.html`, with no build step and no dependencies.

## What is inside

- **Emotion Spectrum Orb.** A canvas orb whose colors, movement and light follow your feelings. A ring around it shows the mix, so several emotions blend into several colors. Tap any of the nine feeling chips to tune it by hand.
- **Nine feeling families.** Happiness, Sadness, Anger, Love, Lust, Fear, Confidence, Curiosity and Complex feelings, plus anything that does not fit. Mixed, shifting and unnamed feelings are supported.
- **Adaptive personality.** The reply tone changes with the feeling: calm for anger, energetic for joy, gentle for sadness, and so on. A "Felt differently?" link under each reply lets the person correct the reading. The reading is never a diagnosis.
- **Mood music, composed live.** Generated in the browser with the Web Audio API, so there is no audio to license. Eleven moods, eight world styles (raga, koto, oud and maqam, flamenco, kalimba, Celtic, gamelan, Latin), repeating melodies that slowly change, play and pause, skip, and volume.
- **My songs.** Add your own audio files, tag each with a feeling, and let SOULSPACE pick a matching one as your mood changes. Files stay in the browser and are gone when the tab closes.
- **Songs on YouTube.** Search links by language and feeling, and a list of saved YouTube links. YouTube cannot be embedded here, so links open in a new tab.
- **Intimacy mode (18+).** Off by default and behind an age confirmation. Conversation stays respectful and non-explicit.
- **Safety.** If someone writes about self-harm, a calm support card appears, the music softens and the AI replies with care. Local phrase detection runs in the browser, and the AI can flag it too.

## Run it

Open `index.html` in a browser. Or serve the folder:

```
python3 -m http.server 8000
```

then visit `http://localhost:8000`.

## Publish on GitHub Pages

1. Push this folder to a GitHub repository.
2. In the repository, open **Settings → Pages**.
3. Under **Build and deployment**, choose **Deploy from a branch**, pick `main` and `/ (root)`, and save.
4. After a minute the page is live at `https://<your-name>.github.io/<repo-name>/`.

## AI replies

The page was built to run inside Claude, where it asks Claude for replies through `window.claude.use("sample")`. Outside Claude that object does not exist, so on GitHub Pages:

- The orb, music, feeling chips, playlist and YouTube finder all work.
- The chat shows a note that replies are not available, and the orb still reacts to the words through the built-in keyword reader (English and Bengali).

To get AI replies on your own site, replace the `sample(turns, {...})` call inside `send()` with a request to a small backend of your own that calls a language model API. Keep the API key on that server and never put it in `index.html`. The model should return the same format the page already parses: a first line of JSON like `{"emotions":[{"category":"sadness","label":"Nostalgia","intensity":0.7}],"crisis":false}`, a blank line, then the reply text. The full instructions given to the model are in the `rules()` function.

## Music and copyright

The built-in music is generated, so nothing needs a license. Songs you add stay on your device. If you ever bundle audio files in this repository, use only public domain, CC0 or other open-licensed tracks, and keep their credits.

## Privacy

The page stores nothing in the browser. Messages go only to whatever backend you connect for replies. "Clear conversation" removes the chat from view.

## Not a medical tool

SOULSPACE reflects feelings back. It is not a doctor or therapist and does not diagnose. If you or someone you know is in danger, contact local emergency services or a trusted person nearby.
