# Four-Frame Landing Page Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Convert 5-frame placeholder landing page to 4-frame video-driven experience

**Architecture:** Replace placeholder gradients with actual MP4 videos, consolidate frames 2-3 into unified services frame, remove frame 5, update navigation to 4 dots

**Tech Stack:** HTML5 video, vanilla CSS, vanilla JavaScript (IntersectionObserver)

---

## Task 1: Update Navigation Dots (5 → 4)

**Files:**
- Modify: `index.html:259-265` (navigation dots)
- Modify: `index.html:363-386` (JavaScript)

**Step 1: Update HTML navigation dots**

Replace the 5-dot navigation with 4 dots:

```html
<!-- Navigation dots -->
<div class="frame-counter">
    <div class="dot active" data-frame="1"></div>
    <div class="dot" data-frame="2"></div>
    <div class="dot" data-frame="3"></div>
    <div class="dot" data-frame="4"></div>
</div>
```

**Step 2: Verify structure**

Open `index.html` in editor and confirm only 4 dots remain in `.frame-counter` div.

**Step 3: Commit**

```bash
git add index.html
git commit -m "refactor: update navigation from 5 to 4 dots"
```

---

## Task 2: Replace Frame 1 Placeholder with Video

**Files:**
- Modify: `index.html:268-289` (Frame 1 section)

**Step 1: Replace video placeholder with actual video**

Replace the `.video-placeholder` div and `.video-note` with actual video element:

```html
<!-- FRAME 1: Hero / Intro -->
<section class="frame frame-1" id="frame1">
    <video class="video-bg" autoplay muted loop playsinline>
        <source src="images/Frame_1__202602121907_e2dgt.mp4" type="video/mp4">
    </video>
    <div class="overlay"></div>

    <div class="content">
        <div class="logo">iatech</div>
        <h1 class="headline">L'informatique.<br>Sans bullshit.</h1>
        <p class="subline">Réparation • IA • Solutions</p>
    </div>

    <div class="location-tag">📍 Saint-Pacôme, Kamouraska</div>

    <div class="scroll-hint">
        <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
            <path d="M7 13l5 5 5-5M7 6l5 5 5-5"/>
        </svg>
    </div>
</section>
```

**Step 2: Verify in browser**

Open `index.html` in browser:
- Expected: Video autoplays and loops
- Expected: Text remains readable over video
- Expected: Logo, headline, subline all visible

**Step 3: Commit**

```bash
git add index.html
git commit -m "feat: add Frame 1 video background"
```

---

## Task 3: Update Frame 2 with Video and Consolidated Services

**Files:**
- Modify: `index.html:291-304` (Frame 2 section)

**Step 1: Replace Frame 2 placeholder and update text**

Update Frame 2 to consolidate repair + AI services:

```html
<!-- FRAME 2: Services -->
<section class="frame frame-2" id="frame2">
    <video class="video-bg" autoplay muted loop playsinline>
        <source src="images/Frame_2__202602121922_af0nv.mp4" type="video/mp4">
    </video>
    <div class="overlay"></div>

    <div class="content">
        <h2 class="headline">Ça marche plus?<br>Ça va marcher.</h2>
        <p class="subline">PC • Portable • Imprimante • IA</p>
    </div>
</section>
```

**Step 2: Verify in browser**

Scroll to Frame 2:
- Expected: Video autoplays when scrolled into view
- Expected: Combined services text visible (includes "IA" in subline)
- Expected: Smooth scroll-snap transition from Frame 1

**Step 3: Commit**

```bash
git add index.html
git commit -m "feat: add Frame 2 video with consolidated services"
```

---

## Task 4: Update Frame 3 with Drone Video (Local Trust)

**Files:**
- Modify: `index.html:306-319` (Frame 3 section)

**Step 1: Replace Frame 3 with drone footage and local content**

Update Frame 3 to use drone video with local trust messaging:

```html
<!-- FRAME 3: Local -->
<section class="frame frame-3" id="frame3">
    <video class="video-bg" autoplay muted loop playsinline>
        <source src="images/frame4Drone_aerial_shot_202602121950_6jq6k.mp4" type="video/mp4">
    </video>
    <div class="overlay"></div>

    <div class="content">
        <h2 class="headline">Ton voisin<br>informatique.</h2>
        <p class="subline">30 ans d'expérience • Service rapide</p>
    </div>

    <div class="location-tag">📍 Saint-Pacôme, Kamouraska</div>
</section>
```

**Step 2: Verify in browser**

Scroll to Frame 3:
- Expected: Drone aerial video autoplays
- Expected: "Ton voisin informatique" headline visible
- Expected: Location tag visible at bottom
- Expected: Video is largest file (8.8MB) so may take moment to load

**Step 3: Commit**

```bash
git add index.html
git commit -m "feat: add Frame 3 drone video with local trust content"
```

---

## Task 5: Update Frame 4 with Contact Video

**Files:**
- Modify: `index.html:321-334` (Frame 4 section - what was old Frame 4)

**Step 1: Replace Frame 4 with contact content and video**

Update the current Frame 4 to become the new contact frame:

```html
<!-- FRAME 4: Contact -->
<section class="frame frame-4" id="frame4">
    <video class="video-bg" autoplay muted loop playsinline>
        <source src="images/Frame_3__202602121925_kdy1j.mp4" type="video/mp4">
    </video>
    <div class="overlay"></div>

    <div class="content">
        <h2 class="headline">On jase?</h2>

        <div class="contact-content">
            <a href="tel:+1234567890" class="contact-link">
                📞 <span>Appelle</span>
            </a>
            <a href="mailto:info@iatechinfo.com" class="contact-link">
                ✉️ <span>Écris</span>
            </a>
            <a href="#" class="contact-link">
                💬 <span>Messenger</span>
            </a>
        </div>
    </div>

    <div class="location-tag">📍 Saint-Pacôme, Kamouraska</div>
</section>
```

**Step 2: Verify in browser**

Scroll to Frame 4:
- Expected: Contact video autoplays
- Expected: "On jase?" headline visible
- Expected: All 3 contact links visible and clickable
- Expected: Location tag at bottom

**Step 3: Commit**

```bash
git add index.html
git commit -m "feat: add Frame 4 contact video and CTAs"
```

---

## Task 6: Remove Frame 5 Entirely

**Files:**
- Modify: `index.html:336-361` (Frame 5 section - DELETE)

**Step 1: Delete Frame 5 HTML section**

Delete the entire Frame 5 section (lines 336-361):

```html
<!-- DELETE THIS ENTIRE SECTION -->
<!-- FRAME 5: Contact -->
<section class="frame frame-5" id="frame5">
    ...entire section...
</section>
```

Remove everything from `<section class="frame frame-5"...` through `</section>`.

**Step 2: Verify in browser**

Scroll through all frames:
- Expected: Only 4 frames exist (can't scroll past Frame 4)
- Expected: Navigation dots show only 4 dots
- Expected: No errors in browser console

**Step 3: Commit**

```bash
git add index.html
git commit -m "refactor: remove Frame 5 section"
```

---

## Task 7: Clean Up CSS

**Files:**
- Modify: `index.html:7-254` (CSS section)

**Step 1: Remove unused video placeholder gradients**

Delete the gradient background CSS for video placeholders (lines 63-81):

```css
/* DELETE THESE SECTIONS */
.frame-1 .video-placeholder { ... }
.frame-2 .video-placeholder { ... }
.frame-3 .video-placeholder { ... }
.frame-4 .video-placeholder { ... }
.frame-5 .video-placeholder { ... }
```

**Step 2: Remove video-placeholder and video-note styles**

Delete unused placeholder styles (lines 49-61 and 217-228):

```css
/* DELETE */
.video-placeholder { ... }

/* DELETE */
.video-note { ... }
```

**Step 3: Verify in browser**

Refresh the page:
- Expected: No visual changes (CSS removal shouldn't affect anything)
- Expected: No console errors
- Expected: Videos still display correctly

**Step 4: Commit**

```bash
git add index.html
git commit -m "refactor: remove unused placeholder CSS"
```

---

## Task 8: Final Verification

**Files:**
- Verify: `index.html` (entire file)
- Verify: Browser console
- Verify: All 4 videos in `images/` folder

**Step 1: Full page test in browser**

Open `index.html` and test:

1. **Frame 1 (Hero)**
   - ✓ Frame_1 video autoplays
   - ✓ Logo visible
   - ✓ "L'informatique. Sans bullshit." headline
   - ✓ Location tag at bottom
   - ✓ Scroll hint animating

2. **Frame 2 (Services)**
   - ✓ Frame_2 video autoplays on scroll
   - ✓ "Ça marche plus? Ça va marcher." headline
   - ✓ "PC • Portable • Imprimante • IA" subline

3. **Frame 3 (Local)**
   - ✓ Drone video autoplays on scroll
   - ✓ "Ton voisin informatique." headline
   - ✓ Experience subline visible
   - ✓ Location tag at bottom

4. **Frame 4 (Contact)**
   - ✓ Frame_3 video autoplays on scroll
   - ✓ "On jase?" headline
   - ✓ All 3 contact links clickable
   - ✓ Location tag at bottom

**Step 2: Navigation test**

- ✓ 4 dots visible on right side
- ✓ Active dot highlights correctly as you scroll
- ✓ Clicking dots navigates to correct frame
- ✓ Smooth scroll-snap behavior

**Step 3: Console check**

Open browser DevTools console:
- Expected: No errors
- Expected: All 4 videos loaded successfully
- Expected: IntersectionObserver working

**Step 4: Mobile test (optional)**

If available, test on mobile device or responsive mode:
- ✓ Videos autoplay (with muted attribute)
- ✓ Text is readable (clamp sizing works)
- ✓ Touch scrolling works smoothly

**Step 5: Final commit**

If any minor adjustments were needed, commit them:

```bash
git add index.html
git commit -m "chore: final verification and adjustments"
```

---

## Success Criteria Checklist

Before marking complete, verify:

- [ ] All 4 video files display correctly
- [ ] Videos autoplay and loop continuously
- [ ] Text overlays are readable on all videos
- [ ] Navigation has exactly 4 dots
- [ ] Active dot updates as you scroll
- [ ] Clicking dots navigates to frames
- [ ] Scroll-snap behavior is smooth
- [ ] All contact links work on Frame 4
- [ ] No Frame 5 exists
- [ ] No console errors
- [ ] No unused CSS remains
- [ ] Page loads quickly (videos compressed)

---

## Notes for Engineer

**Video paths:** All videos are in `images/` folder with exact filenames:
- `Frame_1__202602121907_e2dgt.mp4`
- `Frame_2__202602121922_af0nv.mp4`
- `Frame_3__202602121925_kdy1j.mp4`
- `frame4Drone_aerial_shot_202602121950_6jq6k.mp4`

**No git repo:** This project is not in a git repository, so the commit commands are optional/theoretical. Focus on the implementation steps.

**Video attributes:** Always use `autoplay muted loop playsinline` for TikTok-style autoplay.

**Testing:** Best tested in Chrome/Firefox with DevTools open to monitor video loading.

**Performance:** The drone video (8.8MB) is largest - may take moment to load on slower connections. Consider adding loading state in future if needed.
