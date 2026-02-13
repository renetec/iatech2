# Language Toggle & Logo Replacement Design

**Date:** 2026-02-12
**Project:** iatech informatique landing page
**Goal:** Add English/Spanish language toggle and replace circular logo with actual transparent logo image

---

## Overview

Enhance the 4-frame landing page with bilingual support (French/English/Spanish) and replace the placeholder circular logo with the actual iatech logo image with transparent background.

## Design Decisions

### Default Language
**French** - Primary language for Quebec market (Saint-Pacôme, Kamouraska)

### Toggle Approach
**Fixed Top Corner** - Most discoverable and user-friendly approach

---

## Component 1: Language Toggle

### Placement & Structure
- **Position:** Fixed in top-right corner
- **Format:** `FR | EN | ES` (text-based, clean)
- **Visibility:** Always visible, floats above all content
- **Z-index:** Above videos and all other content

### Visual Design
```
┌─────────────────┐
│  FR | EN | ES   │
└─────────────────┘
```

**Styling:**
- Background: `rgba(255, 255, 255, 0.15)` with `backdrop-filter: blur(10px)` (frosted glass)
- Padding: `0.5rem 1rem`
- Border-radius: `20px`
- Active language: white, bold (font-weight: 700)
- Inactive languages: 50% opacity
- Separator: `|` between languages
- Font-size: `0.9rem`

### Behavior
- **Click any language** → instant switch (no page reload)
- **Text fade transition:** 0.3s ease for smooth language swap
- **Active state:** Bold + full opacity
- **Hover state:** Inactive languages brighten to 70% opacity
- **Session-only:** No localStorage (keeps implementation simple)

### Technical Implementation
- JavaScript object with all translations
- `data-lang` attributes on translatable elements
- Click handler on language buttons
- Function to swap all text content based on selected language

---

## Component 2: Logo Replacement

### Current State
- White circular div with "iatech" text
- CSS creates circle with background

### New State
- Actual logo image: `iatec_logo.png` (converted from JPG)
- Transparent background
- Drop shadow for visibility

### Image Processing
**Convert JPG to PNG with transparency:**
```bash
convert images/iatec_logo.jpg -fuzz 10% -transparent white images/iatec_logo.png
```

- `-fuzz 10%`: Tolerates slight color variations in white background
- `-transparent white`: Makes white pixels transparent
- Output: `iatec_logo.png` with transparent background

### HTML Structure
**Before:**
```html
<div class="logo">iatech</div>
```

**After:**
```html
<img src="images/iatec_logo.png" alt="iatech" class="logo">
```

### CSS Updates
**Remove (from current .logo style):**
- `border-radius: 50%` (no circle)
- `background: #fff` (transparent now)
- `display: flex` / `justify-content` / `align-items` (no centering text)
- `font-weight: bold` (not text anymore)
- `color: #1a1a2e` (not text)
- `font-size: 0.8rem` (not text)

**Add/Update:**
```css
.logo {
    max-width: 150px;
    max-height: 80px;
    width: auto;
    height: auto;
    margin-bottom: 1.5rem;
    filter: drop-shadow(0 4px 12px rgba(0,0,0,0.6));
}
```

**Drop shadow reasoning:**
- Makes logo visible over any video background
- Softer than box-shadow (follows logo shape)
- Dark shadow provides contrast

---

## Component 3: Translation Content

All text content will be stored in a JavaScript translations object with three language keys: `fr`, `en`, `es`.

### Frame 1: Hero/Intro

| Element | French (Default) | English | Spanish |
|---------|------------------|---------|---------|
| Headline | L'informatique.<br>Sans bullshit. | Tech.<br>No bullshit. | Tecnología.<br>Sin rodeos. |
| Subline | Réparation • IA • Solutions | Repair • AI • Solutions | Reparación • IA • Soluciones |

### Frame 2: Services

| Element | French (Default) | English | Spanish |
|---------|------------------|---------|---------|
| Headline | Ça marche plus?<br>Ça va marcher. | Not working?<br>We'll fix it. | ¿No funciona?<br>Lo arreglamos. |
| Subline | PC • Portable • Imprimante • IA | PC • Laptop • Printer • AI | PC • Portátil • Impresora • IA |

### Frame 3: Local Trust

| Element | French (Default) | English | Spanish |
|---------|------------------|---------|---------|
| Headline | Ton voisin<br>informatique. | Your local<br>tech. | Tu técnico<br>local. |
| Subline | 30 ans d'expérience • Service rapide | 30 years experience • Fast service | 30 años de experiencia • Servicio rápido |

### Frame 4: Contact

| Element | French (Default) | English | Spanish |
|---------|------------------|---------|---------|
| Headline | On jase? | Let's talk? | ¿Hablamos? |
| Contact Link 1 | Appelle | Call | Llama |
| Contact Link 2 | Écris | Write | Escribe |
| Contact Link 3 | Messenger | Messenger | Messenger |

### Location Tag
**Unchanged across all languages:**
- `📍 Saint-Pacôme, Kamouraska`

---

## Technical Architecture

### Translation Object Structure
```javascript
const translations = {
    fr: {
        frame1: {
            headline: "L'informatique.<br>Sans bullshit.",
            subline: "Réparation • IA • Solutions"
        },
        frame2: {
            headline: "Ça marche plus?<br>Ça va marcher.",
            subline: "PC • Portable • Imprimante • IA"
        },
        frame3: {
            headline: "Ton voisin<br>informatique.",
            subline: "30 ans d'expérience • Service rapide"
        },
        frame4: {
            headline: "On jase?",
            contact1: "Appelle",
            contact2: "Écris",
            contact3: "Messenger"
        }
    },
    en: { /* same structure */ },
    es: { /* same structure */ }
};
```

### HTML Data Attributes
Add `data-lang-key` attributes to elements that need translation:
```html
<h1 class="headline" data-lang-key="frame1.headline">L'informatique.<br>Sans bullshit.</h1>
<p class="subline" data-lang-key="frame1.subline">Réparation • IA • Solutions</p>
```

### Language Switch Function
```javascript
function switchLanguage(lang) {
    currentLanguage = lang;

    // Update all elements with data-lang-key
    document.querySelectorAll('[data-lang-key]').forEach(el => {
        const key = el.getAttribute('data-lang-key');
        const keys = key.split('.');
        el.innerHTML = translations[lang][keys[0]][keys[1]];
    });

    // Update active language button
    document.querySelectorAll('.lang-btn').forEach(btn => {
        btn.classList.toggle('active', btn.dataset.lang === lang);
    });
}
```

---

## Implementation Checklist

### Phase 1: Logo Replacement
- [ ] Convert `iatec_logo.jpg` to `iatec_logo.png` with transparent background
- [ ] Update HTML: replace logo div with img tag
- [ ] Update CSS: remove circle styles, add image sizing and drop shadow
- [ ] Verify logo displays correctly over videos

### Phase 2: Language Toggle UI
- [ ] Add language toggle HTML in top-right corner
- [ ] Add CSS for frosted glass effect and active states
- [ ] Position toggle with fixed positioning

### Phase 3: Translation System
- [ ] Create translations JavaScript object with all content
- [ ] Add `data-lang-key` attributes to all translatable elements
- [ ] Implement `switchLanguage()` function
- [ ] Add click handlers to language buttons
- [ ] Test all three languages across all frames

### Phase 4: Verification
- [ ] Test language switching on all frames
- [ ] Verify logo transparent background works
- [ ] Check responsive behavior (mobile/tablet)
- [ ] Verify no layout shifts when switching languages
- [ ] Test hover states on language toggle

---

## Design Principles

**Minimal Impact:**
- Language toggle is small and unobtrusive
- Transparent logo blends naturally with video backgrounds
- No layout changes, just content swapping

**User-Friendly:**
- Toggle always accessible (fixed position)
- Clear language labels (FR/EN/ES)
- Instant switching (no page reload)
- Smooth transitions

**Maintainable:**
- All translations in one central object
- Data attributes make adding new translatable elements easy
- Simple JavaScript, no framework dependencies

---

## Success Criteria

- [ ] Language toggle visible and functional on all frames
- [ ] Three languages switch instantly with smooth transition
- [ ] French is default language on page load
- [ ] Logo displays with transparent background and drop shadow
- [ ] Logo visible over all video backgrounds
- [ ] All text translates correctly (no missing translations)
- [ ] Layout remains stable across language switches
- [ ] No console errors
- [ ] Works on mobile and desktop

---

## Future Enhancements (Not in Current Scope)

- LocalStorage to remember language preference
- Browser language auto-detection
- Fade animation for text transitions
- Keyboard shortcuts for language switching
- Additional languages (Portuguese for Brazilian market?)
