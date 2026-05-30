# supreme-carnival

A [HyperFrames](https://hyperframes.heygen.com) project for creating, previewing, and
rendering videos from HTML/CSS/animations into deterministic MP4s.

## Prerequisites

- **Node.js 22+**
- **FFmpeg** (`ffmpeg` + `ffprobe` on PATH)

## Project

The composition project lives in [`my-video/`](./my-video). All commands run from there:

```bash
cd my-video

npm run dev      # preview studio in the browser with live reload (long-running)
npm run check    # lint + validate (headless Chrome) + inspect layout
npm run render   # render to MP4 -> my-video/renders/
npm run publish  # publish and get a shareable link
```

Edit `my-video/index.html` (the root composition) to build your video. See
`my-video/CLAUDE.md` for the authoring rules and the installed AI agent skills.

## First-time setup after cloning

```bash
cd my-video
npm install                                   # restores gsap (and other deps)
npx skills add heygen-com/hyperframes         # restores the AI agent skills (.agents/)
```

## Environment note: local GSAP instead of CDN

This environment's network policy blocks public CDNs (e.g. `cdn.jsdelivr.net`), so the
default CDN `<script>` for GSAP is replaced with a **local** reference served from the
installed npm package:

- `gsap` is a dependency in `my-video/package.json`
- `index.html` loads it as `./node_modules/gsap/dist/gsap.min.js`

So `npm install` is required before previewing/rendering. If you add other libraries
(Lottie, Three.js, Anime.js, …), add them as npm dependencies and reference them from
`./node_modules/...` the same way rather than loading from a CDN — otherwise the
headless-Chrome validate/render steps fail with `ERR_CERT_AUTHORITY_INVALID` /
`host_not_allowed`.
