# YouTube Music Enhancer — Project Plan

## Project Overview
A Firefox browser extension that adds missing audio features to YouTube Music:
- **Equalizer** (5-10 band)
- **Crossfader** (automatic fade-between-tracks and/or manual control)

**Scope**: Long-term hobby project. Start with MVP (basic EQ + crossfader), iterate.

---

## Architecture Decision: Browser Extension ✓

| Aspect | Decision | Rationale |
|--------|----------|-----------|
| **Format** | Firefox browser extension | Simpler than standalone app; proven by existing extensions (YouTube Playlist Crossfade, eq-for-youtube) |
| **Tech Stack** | JavaScript + Web Audio API + Firefox extension APIs | No backend needed; Web Audio API proven to work with YouTube Music streams |
| **Storage** | Firefox `chrome.storage.sync` | User settings persist locally, sync across their Firefox installations |
| **Distribution** | Firefox Add-ons marketplace | One-click install for users; GitHub for development |

---

## Technical Feasibility

### Audio Access: POSSIBLE ✓
- YouTube Music's audio is accessible via **Web Audio API** after the browser decodes it
- Existing extensions successfully implement EQ and crossfading
- No YouTube Music official API needed; extensions intercept playback

### Known Constraints
- YouTube Music doesn't have a public audio API—we work around it
- Extension depends on YouTube Music's HTML/interface stability
- YouTube updates can break extensions; robustness required

### Research References
- Existing extensions: YouTube Playlist Crossfade, Music Speed Changer, eq-for-youtube
- Key tech: Web Audio API biquad filters for EQ, scheduling API for crossfade timing

---

## Development Environment

**Local Setup**
- Machine: Mac (M1/Intel)
- Editor: VS Code
- Version Control: GitHub
- Browser: Firefox (Developer Edition preferred)
- Cloud: AWS account available (not needed for MVP)

**Workflow**
1. Edit extension code in VS Code
2. Load extension in Firefox via `about:debugging` → "Load Temporary Add-on"
3. Firefox auto-reloads on save (with proper setup)
4. Debug via Firefox DevTools

---

## Repository Structure

youtube-music-enhancer/
├── src/
│   ├── manifest.json          (extension metadata)
│   ├── content-script.js      (injects UI, hooks Web Audio API)
│   ├── background.js          (if needed for persistent logic)
│   ├── styles.css
│   └── icons/
├── tests/                     (add later)
├── docs/
│   └── README.md
├── .gitignore
└── AGENTS.md                  (this file)


---

## Next Steps (Prioritized)

### Phase 1: Proof of Concept
- [ ] Set up Firefox extension "Hello World" (manifest.json + content script)
- [ ] Inject a test button into YouTube Music UI
- [ ] Verify Firefox reload cycle works smoothly
- [ ] Push initial structure to GitHub

### Phase 2: Web Audio API Integration
- [ ] Hook into YouTube Music's audio stream via Web Audio API
- [ ] Implement a single EQ band (e.g., 100Hz) as proof-of-concept
- [ ] Verify audio processing works without breaking playback
- [ ] Test on Mac system audio

### Phase 3: MVP Features
- [ ] Build 5-band equalizer UI (sliders)
- [ ] Implement crossfader logic (automatic or manual TBD)
- [ ] Add preset support (save/load EQ settings)
- [ ] Basic settings storage via `chrome.storage.sync`

### Phase 4: Polish & Distribution
- [ ] Error handling and robustness
- [ ] Firefox Add-ons marketplace submission
- [ ] Documentation for users

---

## Open Design Decisions

Before starting Phase 1, decide on:

1. **UI Placement**
   - Floating panel over YouTube Music?
   - Sidebar?
   - Inject into YouTube Music's native settings?

2. **Crossfader Behavior**
   - Automatic fade between tracks?
   - Manual slider control?
   - Both?

3. **EQ Configuration**
   - 5-band (standard)?
   - 10-band (advanced)?
   - Presets (e.g., "bass boost," "vocal enhance")?

4. **Testing Strategy**
   - How will you catch YouTube Music updates that break the extension?
   - Plan for robustness/monitoring?

---

## Resources to Research

- [ ] Existing extension: `eq-for-youtube` (GitHub source)
- [ ] Firefox WebExtension documentation
- [ ] Web Audio API biquad filter documentation
- [ ] Firefox `chrome.storage.sync` API

---

## Notes

- **AWS**: Not needed for MVP; consider only if adding cloud-based presets or analytics later
- **Licensing**: Working around YouTube Music's DRM is in a gray area legally; however, similar extensions exist on Firefox Add-ons marketplace without issues
- **Long-term**: If successful, could potentially build a standalone Electron app variant later

---

**Last Updated**: August 16, 2026  
**Status**: Planning phase
