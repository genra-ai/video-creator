---
name: genra:news-broadcast
description: "Use this skill when the user wants to create a news broadcast video with an anchor in a TV studio, with optional B-roll shots and reference-photo-based character fidelity. Triggered by: 'news broadcast', '新闻播报'."
---

# News Broadcast Video

Generate a news broadcast video featuring a single anchor in a professional TV studio. Supports reference-photo-based character fidelity, mixed anchor + B-roll structure, and smart tail-frame strategy to prevent character drift at cuts.

## Key Principles

- **Character reference photo is mandatory**: every anchor shot's visual description must begin with `参考原图 $asset_id` — this is the only way to preserve appearance across shots
- **No close-ups on the anchor**: minimum framing is medium shot (waist-up). Close-ups cause character/outfit/environment inconsistency at cuts and don't match broadcast conventions
- **Studio must be explicitly described in EVERY anchor shot**: Do NOT rely on the environment anchor paragraph alone — each anchor shot's 画面描述 must contain the full studio sentence word-for-word identical across all shots. Omitting it from even one shot will cause the AI to invent a different background ("穿帮"). Copy-paste the studio sentence; never paraphrase it.
- **Two shot types, two tail-frame rules**:
  - **Anchor shots (consecutive)**: set tail frames — each anchor shot's tail = next anchor shot's start frame
  - **B-roll shots (event cutaways)**: NO tail frames — the anchor shot before a B-roll does NOT get a tail frame; the B-roll itself does NOT get a tail frame. Hard cuts are correct for news
- **Send all shots + dialogs in one message**
- **Audio before video**

## Shot Type Reference

| Type | When to Use | Framing | Reference Photo |
|------|------------|---------|-----------------|
| 开场走位 Opening entrance | First shot — anchor walks to position | Wide → Medium (Dolly out) | Required |
| 标准播报 Standard reporting | Main anchor delivery shots | Medium (waist-up) | Required |
| 演播室广角 Wide studio | Emphasis, transitions, closing | Wide shot | Required |
| B-roll 事件 Event cutaway | Illustrate news content (documents, objects, locations) | Any (often Close-up) | NOT used |
| 结尾致意 Closing | Final farewell shot | Wide or Medium | Required |

## Workflow

### 1. Analyze Script & Classify Shots

Go through the user's storyboard and assign each shot a type from the table above. Then self-verify:

- Is every shot with a speaking anchor classified as 标准播报/开场走位/结尾致意?
- Is every shot without the anchor (documents, locations, objects, screens) classified as B-roll?
- Are there any ambiguous shots (e.g., anchor looking at LED wall but still on screen)? → classify as anchor shot, not B-roll

Build the tail-frame plan immediately after classification:

```
开场走位: Shot 1
标准播报: Shots 2, 4, 5, 8
B-roll: Shots 3, 6, 7
结尾致意: Shot 9

Tail-frame plan:
  Shot 1 → Shot 2 ✅ (anchor→anchor)
  Shot 2 → no tail ❌ (next is B-roll Shot 3)
  Shot 3 → no tail ❌ (B-roll)
  Shot 4 → Shot 5 ✅ (anchor→anchor)
  Shot 5 → no tail ❌ (next is B-roll Shot 6)
  ...
```

Self-check the plan: every B-roll boundary (anchor→B-roll or B-roll→anchor) must have no tail frame. Fix before proceeding.

### 2. Prepare Character & Scene Description

**Upload reference photo first** (if not already uploaded), record the `asset_id`.

**Character description** (extract from reference photo):
`[age + gender] + [hair: length/texture/color] + [skin tone] + [outfit: color/cut/material] + [one signature detail]`

Example: `25岁女性，肩长微卷发，浅棕色，白皙皮肤，深藏青色专业套装，耳钉`

Signature detail (earring, glasses, hair pin) is the cross-shot anchor — **be precise**: "深藏青色（非黑色）", "纯白（如打印纸）".

**Studio scene description** (keep identical across all anchor shots):
`[studio type] + [background LED wall content] + [light setup] + [key props]`

Standard: `现代电视演播室，背景大型LED显示屏（蓝色调新闻图形），三点专业演播室灯光（冷白5500K），主播台或站立位，地面轻微反光`

LED wall can change content per shot (maps, graphics, case images) — describe what it shows in each shot's description.

### 3. Create Project & Send Script

Send one message with all shots. Begin the message with a **standalone environment anchor paragraph** before listing any shots — this locks the studio into the AI's context so every anchor shot shares the same spatial reference:

```
【演播室环境锚定】
现代专业电视演播室。主播站立于演播室中央偏前位置，正对摄像机方向。背景是一面大型弧形LED显示屏，屏幕显示蓝色调新闻频道图形界面，可随新闻内容切换画面。地面为深色哑光地板，有轻微镜面反光。三点专业演播室灯光：主灯（冷白5500K，正面柔光），侧补光（轻微暖调），背景灯（蓝紫色勾勒轮廓）。演播室纵深感明显，远景略有虚化。整体氛围：专业、严肃、现代感。
```

This paragraph is not a shot — it is environmental context only. Then list shots below it.

Structure each anchor shot as:

```
【镜头N 约Xs】
画面描述：参考原图 $asset_id，保留面部特征、发型、服装。[镜头运动]：[场景动作]。现代专业电视演播室，主播站立于演播室中央偏前，背景大型弧形LED显示屏显示[本镜内容，如蓝色调新闻图形/地图/案例图片]，深色哑光地板轻微镜面反光，三点专业演播室灯光（主灯冷白5500K正面柔光，侧补光轻微暖调，背景蓝紫轮廓灯），演播室纵深感明显，远景略有虚化。主播[情绪/姿态]。
台词：[dialog text]
```

> ⚠️ **穿帮防止规则**：画面描述中的演播室描述句必须在所有主播镜头中**一字不差**复用（仅 LED 屏内容可变）。禁止在不同镜头中用不同词汇描述同一演播室（如一个用"演播室"，另一个用"新闻直播间"）——措辞差异会导致 AI 生成截然不同的背景环境。

Structure each B-roll shot as:

```
【镜头N 约Xs B-roll】
画面描述：[电影感特写/场景描述，无主播出现]。[镜头运动]。[光效/氛围]。
台词：[dialog or 无台词]
```

Include in the message:
- Art style: `写实真人，写实电影感，专业演播室灯光，自然真实质感`
- All anchor shots: same character, same studio environment
- Anchor shots: minimum medium shot (waist-up), character occupying 60–70% of frame height
- No close-up or extreme close-up on the anchor's face
- Camera movement descriptions for each shot (see reference table below)

### 4. Filter Check

- All anchor shots share the same `character_id` and `location_id`
- `identity_anchor` description is **word-for-word identical** across all anchor shots — fix with `edit` if different
- Confirm framings: no anchor shot is parsed as close-up; fix immediately
- Each dialog shot duration ≥ natural reading time + 0.5s

### 5. Check Image Consistency (Anchor Shots Only)

Use Shot 1 as baseline. For each subsequent anchor shot, compare:

| Check | Common Issue | Fix |
|-------|-------------|-----|
| **Studio layout** | Different room shape, desk style, or studio size | **Priority fix**: regenerate with full studio sentence + "演播室布局、空间纵深、地板、背景灯光与镜头1完全一致" |
| **LED wall style** | Background graphic style changes (color, layout, font) | Regenerate; add "背景LED屏幕风格与第一个主播镜头保持一致，仅内容切换为[X]" |
| Outfit color | Navy → black, white → off-white | Regenerate with color reference ("深藏青色，非黑色") |
| Hair length/style | Long becomes short | Regenerate; re-emphasize hair length |
| Shot size / framing | Pushed too close (half-face) | Regenerate; add "中景，腰部以上" to description |
| Depth of field | Background blur level shifts | Root cause of push/pull feel between shots |
| Glazed eyes | Occasional | I2I: "眼神清晰有神，无玻璃质感" |

**Studio consistency is the highest priority** — a character outfit difference is cosmetically jarring, but a background that changes between shots looks like a different location entirely (穿帮). Fix all studio inconsistencies before accepting the image set.

Retry at most once per shot; if still off, accept and move on. Skip B-roll shots in this check — they don't need character consistency.

### 6. Set Tail Frames (Selective)

**Rule**: tail frames only between consecutive anchor shots. Never on B-roll boundaries.

**Procedure**:

1. `get_state` → record each **anchor** shot's `start_frame` asset_id (skip B-roll shots)
2. Build the tail-frame plan based on the classification from Step 1:

```
主播连续转场 (set tail frame):
  Shot 1 tail → Shot 2 start_frame
  Shot 2 tail → Shot 4 start_frame   ← skip Shot 3 (B-roll)

主播→B-roll 或 B-roll→主播 (no tail frame):
  Shot 3 (B-roll): no tail frame
  Shot 5 tail → Shot 6 start_frame   ← if 5→6 are both anchor
  Shot 6 (B-roll): no tail frame
```

3. Set each tail frame one at a time; `get_state` after each to verify `tail_frame` is set. Retry up to 3 times if not confirmed.

### 7. Generate Audio

**Voice description for news anchor**: `[gender + age] + 播音腔 + 清晰干净 + [emotional tone] + 语速适中偏快 + 标准普通话`

| Tone | Example |
|------|---------|
| 正式新闻播报 | 女声，25岁，清晰干净播音腔，专业沉稳，语速适中偏快，标准普通话 |
| 严肃警示内容 | 女声，成熟，低沉有力，语速适中，字字清晰有力 |
| 轻松民生资讯 | 女声，年轻，明亮亲切，自然语速，偶有停顿 |

Voice cloning: upload 5–10s reference audio; use the returned asset_id as the character's voice field.

Generate BGM separately if needed: `新闻背景音乐，低调弦乐+电子底鼓，BPM 90，专业严肃感，不抢人声`

### 8. Generate Videos

After all audio completes, generate all videos.

### 9. Preview & Export

Check anchor-to-anchor transitions first:
- Character appearance (hair, outfit, signature detail) matches across cuts
- No push/pull feel (depth of field consistent)
- No jump in character position/size

Check B-roll cuts:
- Hard cuts are expected and correct — do NOT re-add tail frames to fix them
- B-roll content is visually coherent with the narration

If an anchor-to-anchor transition has a character jump: reset that shot's tail frame and regenerate only that shot's video.

---

## Camera Movement Reference for News Broadcast

| Movement | Chinese | Use Case |
|----------|---------|----------|
| Dolly out (开场跟退) | 斯坦尼康后退镜 | Opening walk-in: anchor approaches camera, lens pulls back |
| Slow push-in | 缓慢推镜头 | Tense/serious news; deepens gravitas |
| Static medium | 固定中景 | Standard reporting; most anchor shots |
| Dolly sideways | 横移镜头 | Directing attention to LED wall content |
| Pull back | 拉镜头 | Revealing studio context; transitions to wide |
| Orbital/arc | 旋转环绕镜头 | Closing shot; shows full studio |
| B-roll rack focus | 拉焦特写 | Documents, objects — focus shifts between subjects |
| B-roll static close-up | 固定特写 | Evidence items, screens, maps |

## Shot Duration Guidelines

| Shot Type | Recommended Duration |
|-----------|---------------------|
| 开场走位 Opening | 6–10s |
| 标准播报 Reporting | Dialog length + 1s buffer |
| B-roll 事件 | 4–6s (no dialog); or dialog length + 0.5s |
| 结尾致意 Closing | 4–6s |
| Total video | 45–90s typical for news segment |
