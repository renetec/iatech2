# Four-Frame TikTok-Style Landing Page Design

**Date:** 2026-02-12
**Project:** iatech informatique landing page
**Goal:** Simplify 5-frame placeholder design to 4 frames with actual video content

## Overview

Transform the current 5-frame TikTok-style vertical scrolling landing page into a streamlined 4-frame experience using actual MP4 videos. Maintain minimal text overlays and smooth scroll-snap behavior while removing placeholder content.

## Design Approach: Classic Marketing Funnel

**Selected Approach:** Hero → Services → Local Trust → Contact

This follows the traditional marketing funnel optimized for social media-style storytelling:
1. Grab attention with brand intro
2. Deliver value with services
3. Build trust with local credentials
4. Convert with clear contact options

## Frame Structure

### Frame 1: Hero/Brand Intro
**Video:** `Frame_1__202602121907_e2dgt.mp4` (2.2MB)

**Content:**
- Logo circle: "iatech"
- Headline: "L'informatique. Sans bullshit."
- Subline: "Réparation • IA • Solutions"
- Location tag: "📍 Saint-Pacôme, Kamouraska"
- Scroll hint indicator (animated chevron)

**Purpose:** Immediate brand recognition and value proposition

---

### Frame 2: Services
**Video:** `Frame_2__202602121922_af0nv.mp4` (2.1MB)

**Content:**
- Headline: "Ça marche plus? Ça va marcher."
- Subline: "PC • Portable • Imprimante • IA"

**Purpose:** Consolidate repair and AI services into one compelling frame

**Note:** Combines what were previously two separate frames (Repair + AI) into a unified services message

---

### Frame 3: Local Trust
**Video:** `frame4Drone_aerial_shot_202602121950_6jq6k.mp4` (8.8MB)

**Content:**
- Headline: "Ton voisin informatique."
- Subline: "30 ans d'expérience • Service rapide"
- Location tag: "📍 Saint-Pacôme, Kamouraska"

**Purpose:** Build local credibility with aerial drone footage of Saint-Pacôme

**Note:** Uses the impressive drone footage to reinforce local presence and trust

---

### Frame 4: Contact/CTA
**Video:** `Frame_3__202602121925_kdy1j.mp4` (5.8MB)

**Content:**
- Headline: "On jase?"
- Three contact buttons:
  - 📞 Appelle (phone link)
  - ✉️ Écris (email link)
  - 💬 Messenger (messenger link)

**Purpose:** Clear call-to-action with multiple contact options

---

## Technical Implementation

### Video Integration
- Replace all `.video-placeholder` divs with `<video>` elements
- Video attributes: `autoplay muted loop playsinline`
- CSS: `object-fit: cover` to fill frame
- Maintain dark overlay (rgba(0,0,0,0.4)) for text readability
- Video paths: `images/[filename].mp4`

### Navigation Updates
- Update `.frame-counter` from 5 dots to 4 dots
- Update observer to track 4 frames instead of 5
- Maintain scroll-snap-type on html element
- Keep clickable dot navigation

### Content Removal
- Delete entire Frame 5 HTML section
- Remove `.frame-5` CSS rules
- Remove all `.video-placeholder` gradient backgrounds
- Remove all `.video-note` elements (red "📹 TON VIDEO ICI" tags)
- Remove unused placeholder emoji (🎬, 🔧, 🤖, 🏘️, 👋)

### Styling Preservation
- Keep responsive text sizing (clamp functions)
- Keep text shadows for video overlay readability
- Keep frame counter styling and animations
- Keep scroll hint animation (bounce)
- Keep CTA button hover effects

### Performance Considerations
- Videos are pre-compressed (2-9MB range, suitable for web)
- Browser native autoplay/loop handles playback efficiently
- No additional JavaScript libraries required
- Existing IntersectionObserver handles scroll detection

## What's Being Consolidated

**Removed from original 5-frame design:**
- Frame 2 (Repair) + Frame 3 (AI) → merged into new Frame 2 (Services)
- Frame 4 (Local) → becomes new Frame 3 with drone footage
- Frame 5 (Contact) → becomes new Frame 4

**Result:** Tighter, more focused user journey with less scrolling

## User Flow

1. User lands on page → **Frame 1** auto-plays with brand intro
2. User scrolls → **Frame 2** shows services with problem/solution hook
3. User scrolls → **Frame 3** builds trust with local drone footage
4. User scrolls → **Frame 4** presents clear contact options
5. User clicks contact method → conversion

**Total scroll depth:** 4 frames (400vh) vs original 5 frames (500vh)

## Design Principles

- **Minimal text:** TikTok/Reels style with short, punchy headlines
- **Video-first:** Content drives the experience, text supports
- **Smooth navigation:** Scroll-snap creates app-like experience
- **Mobile-optimized:** Responsive text sizing, touch-friendly
- **Fast loading:** Compressed videos, no external dependencies

## Success Criteria

- All 4 videos autoplay and loop correctly
- Text remains readable over all video backgrounds
- Navigation dots accurately reflect current frame
- Smooth scroll-snap behavior on all devices
- Contact links functional on Frame 4
- No console errors or performance issues

## Future Considerations

- Monitor video file sizes if adding more content
- Consider lazy-loading videos below fold for performance
- May want to add pause/play controls for accessibility
- Could add analytics tracking for scroll depth and contact clicks
