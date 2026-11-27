# markdown_kit X Promo Video

Reproducible 60-second (1920×1080, 30fps, English voiceover + subtle ambient BGM) promo video for `markdown_kit`, recorded from the live example app and composited with [kasaneru](https://github.com/K9i-0/kasaneru).

## Reproduction steps

1. Ensure the example web app is built:
   ```bash
   cd example && flutter build web --release
   ```
2. Record real screen footage (mobile chat, desktop editor, desktop showcase):
   ```bash
   node tool/promo/record.mjs all
   ```
3. Generate English male narration (`gemini-2.5-flash-preview-tts`, voice `Charon`) and subtle ambient tech BGM (`lyria-002`) via Vertex AI:
   ```bash
   node tool/promo/generate_audio.mjs all
   ```
4. Build `manifest.json` from probed clip & audio durations:
   ```bash
   node tool/promo/build.mjs
   ```
5. Validate and render with `kasaneru`:
   ```bash
   node /Users/kotahayashi/Workspace/kasaneru/bin/kasaneru.mjs check tool/promo/manifest.json
   node /Users/kotahayashi/Workspace/kasaneru/bin/kasaneru.mjs render tool/promo/manifest.json \
     -o tool/promo/final_x_promo.mp4 --crf 17
   ```
6. Inspect & generate review contact sheet:
   ```bash
   node /Users/kotahayashi/Workspace/kasaneru/bin/kasaneru.mjs inspect tool/promo/final_x_promo.mp4 --deep
   node /Users/kotahayashi/Workspace/kasaneru/bin/kasaneru.mjs sheet tool/promo/final_x_promo.mp4 \
     --manifest tool/promo/manifest.json -o tool/promo/out/audit_sheet.png
   ```

Raw recordings (`raw/`), generated audio (`audio/`), intermediate/final renders (`out/`, `*.mp4`), and `*.work/` folders are gitignored.
