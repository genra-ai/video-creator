---
name: sports-action
description: "Use this skill when the user wants to create a sports or athletic action video — athlete highlights, extreme sports, motorsports, fitness training, sports event moments, or any content where physical motion, speed, and athletic performance are the primary subject. NOT for brand story videos that happen to feature athletes. NOT for cinematic trailers using sports as a dramatic backdrop. Triggered by: 'sports video', 'athlete highlight', 'extreme sports', 'training video', 'race video', 'sports reel', 'workout video', 'match highlight', 'skateboarding video', 'fitness video', 'sports montage', '运动视频', '体育视频', '训练视频', '极限运动', '比赛集锦', '运动员宣传片'."
---

# Sports Action

Creates sports and athletic action videos where physical performance is the story. The content is kinetic, visceral, and built around the peak moments of athletic motion — the sprint, the impact, the landing, the split-second of maximum effort.

## Key Principles

- **Peak moment is the frame**: every shot is built around the most visually intense instant of the action, not a neutral position
- **Motion conveys meaning**: speed blur, camera angle, and timing carry the emotional weight — describe these precisely
- **Environment is part of the story**: stadium lights, track surface, snow spray, gym chalk — the setting amplifies the performance
- **No narration required**: sports action stands alone; dialog or voiceover is optional and additive, not structural
- **No tail frames; BGM before video**

## Workflow

### 1. Identify Sport Type and Content Goal

After the user describes the video, identify:

| Element | What to determine |
|---|---|
| **Sport / activity** | Team sport / individual sport / extreme / motorsports / fitness & training / martial arts / dance-athletic |
| **Content goal** | Highlight reel / single peak moment / athlete profile / training montage / event recap / motivational content |
| **Tone** | Adrenaline-driven / inspirational / technical showcase / raw and gritty / cinematic epic |
| **Reference media available?** | If user uploads action photos or clips, these become start-frame anchors |

If the sport type or main subject is ambiguous, ask one focused question. Do not ask for details that can be inferred.

### 2. Select Content Structure

| Structure | Shots | Best For |
|---|---|---|
| **Single peak moment** | 1–2 | One defining action: the dunk, the jump, the collision — build-up + peak or peak + aftermath |
| **Highlight sequence** | 3–5 | Multiple distinct actions from the same sport or athlete, connected by pace and rhythm |
| **Training montage** | 4–6 | Progressive effort build — warm-up → drill → full intensity → exhaustion/triumph |
| **Athlete profile** | 3–5 | Introduce the athlete, show their sport, end on a defining moment — character-driven |
| **Event moment** | 2–4 | Capture the atmosphere and key instant of a specific competition or event |

### 3. Camera Language for Sports

Sports action requires specific camera choices. Use the vocabulary below:

**Shot scale and angle**:

| Angle / Scale | Effect | Use When |
|---|---|---|
| Low angle, wide lens (Dutch tilt optional) | Amplifies power and scale | Sprinter launch, weightlifter lockout, biker takeoff |
| Eye-level tracking shot | Places viewer in the action | Running alongside athlete, following a ball |
| High overhead / drone-style | Shows spatial scale and formation | Team play, racing track layout, mountain descent |
| Extreme close-up | Reveals physical detail and strain | Grip on bar, cleats on track, exhale through mouthguard |
| Slow-motion freeze | Isolates the peak millisecond | Ball at moment of impact, foot at moment of plant |

**Camera motion**:

| Motion | Use When |
|---|---|
| Fast pan / whip pan | Transitions between locations or moments with energy |
| Tracking follow | Athlete moving laterally, conveys speed through parallel motion |
| Push-in to close-up | Moment of peak intensity — narrows focus as effort peaks |
| Locked-off static | Deliberate stillness that makes the subject's motion MORE dramatic by contrast |
| Handheld / slight shake | Raw, in-the-moment authenticity for training or gritty content |

### 4. Motion Description Rules

Each shot must describe **three layers of motion**:

1. **Athlete motion**: what the body is doing at the captured instant (not the full sequence — the peak frame)
2. **Environment motion**: what else moves (crowd blur, dust, water splash, equipment swing)
3. **Camera motion**: how the camera itself moves, and at what speed relative to subject

**Speed treatment**:

| Speed Style | How to Describe |
|---|---|
| Real-time high energy | "fast handheld track, motion blur on background, athlete sharp" |
| Slow motion peak | "overcranked at peak impact, time slows to isolate body position" |
| Ramping (slow → fast) | "begins in slow motion as athlete crouches, accelerates to real-time on release" |

### 5. Build Shot Descriptions

Each shot description must include all of the following:

- **Athlete/subject**: build, posture at the captured moment, gear/kit color and style
- **Peak action state**: the exact physical position at the frame's key instant
- **Environment**: surface, backdrop, ambient conditions (lighting, weather, crowd)
- **Camera angle and motion**: as specified in Step 3
- **Speed/motion treatment**: real-time / slow-mo / ramp, and what has motion blur
- **Atmosphere/energy**: visual cues of intensity (sweat droplets, chalk cloud, tire smoke, breath mist)

Do NOT describe what the athlete "achieves" or "feels" — only what is physically visible in the frame.

**Example**:
```
Shot 2 (6s): Low angle looking up, wide lens. A male sprinter in black compression shorts and
a red singlet explodes from starting blocks — both hands just lifted off the track surface,
rear leg fully extended, front knee driving forward. Track surface fills the lower third of
frame. Stadium floodlights create lens flare from top right. Motion blur on the sprinter's
trailing limbs; face and forward knee sharp. Slow-motion ramp from freeze-frame on foot
plant to real-time at full extension. Dust particles visible at track level.
```

### 6. Sport-Specific Visual Reference

| Sport Category | Key Visual Signatures |
|---|---|
| **Track & field** | Starting block explosion, lean at finish tape, hurdle clearance geometry, javelin arc |
| **Ball sports (soccer/basketball/football)** | Ball at moment of contact, athlete mid-air with ball relation, goal-line/rim moments |
| **Extreme sports (skate/surf/snow)** | Board separation from ground, aerial body rotation, lip of wave curl, powder spray |
| **Motorsports** | Tire smoke, apex geometry, helmet visor reflection, G-force visible in body position |
| **Martial arts / combat** | Limb extension at full reach, contact-point freeze, guard stance at peak tension |
| **Fitness / training** | Bar at lockout, muscle definition under gym light, chalk dispersal, sweat detail |
| **Cycling / running** | Cadence at peak effort, gradient and terrain relationship, peloton/pack geometry |

### 7. Image Input Handling

If the user provides action photos:
- Use as **start frame** (`$asset_id`) for the corresponding shot
- Description must begin from the state shown in the photo and describe how the motion evolves forward from that frame
- Do not re-describe what is static in the image — describe only motion and change

### 8. Script Format

```
Sport: [sport / activity type]
Content structure: [single peak moment / highlight sequence / training montage / athlete profile / event moment]
Tone: [adrenaline-driven / inspirational / technical / gritty / cinematic epic]
BGM: [style, BPM — e.g., "high-energy electronic, BPM 130–150" or "orchestral build, no lyrics"]
Resolution: [1280×720 / 720×1280]

Shot 1 (Xs): [athlete state + action + environment + camera + motion treatment + atmosphere]
Shot 2 (Xs): [athlete state + action + environment + camera + motion treatment + atmosphere]
...
```

### 9. Filter Check

Before generating, confirm:

- Every shot contains: subject at peak action + camera specification + motion treatment
- Speed treatment is consistent with the tone (slow-mo for epic, real-time for raw)
- No shot describes outcome or emotion — only visible physical state
- Total duration: 8–45 seconds (highlight reels up to 60s)
- No tail frames

### 10. Clear All Tail Frames

### 11. BGM Selection

BGM drives the kinetic rhythm — choose before video generation.

| Tone | BGM Style | BPM |
|---|---|---|
| Adrenaline / high intensity | Electronic / trap / hard rock, driving beat | 130–160 |
| Inspirational / motivational | Orchestral build or cinematic hip-hop | 90–120 |
| Raw / underground / gritty | Lo-fi hip-hop, distorted guitar, no polish | 80–110 |
| Cinematic epic | Full orchestral, swelling strings, percussive hits | 60–90 |
| Technical / skill showcase | Minimal electronic, sparse, lets motion breathe | 100–120 |

### 12. Generate Videos

No voiceover unless the user specifically requested it. BGM only by default. Generate all shots, then export.

---

## Resolution

| Use Case | Resolution |
|---|---|
| Landscape — YouTube, event screen, horizontal reel | 1280×720 (16:9) — default |
| Portrait — TikTok, Instagram Reels, vertical highlight | 720×1280 (9:16) |
| Square — Instagram feed post | 720×720 (1:1) |
