# Language Toggle & Logo Replacement Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Add trilingual support (FR/EN/ES) with toggle button and replace placeholder logo with actual transparent logo image

**Architecture:** Client-side language switching using JavaScript translations object with data attributes, ImageMagick for logo background removal, CSS-only toggle UI with frosted glass effect

**Tech Stack:** HTML5, vanilla CSS, vanilla JavaScript, ImageMagick (for image processing)

---

## Task 1: Convert Logo to PNG with Transparent Background

**Files:**
- Input: `images/iatec_logo.jpg`
- Output: `images/iatec_logo.png`

**Step 1: Verify ImageMagick is installed**

```bash
convert --version
```

Expected: Version info displayed (ImageMagick 6.x or 7.x)

**Step 2: Convert JPG to PNG with transparency**

```bash
convert images/iatec_logo.jpg -fuzz 10% -transparent white images/iatec_logo.png
```

- `-fuzz 10%`: Handles slight color variations in white background
- `-transparent white`: Makes all white pixels transparent

Expected: New `iatec_logo.png` file created

**Step 3: Verify PNG has transparency**

```bash
identify -verbose images/iatec_logo.png | grep -i alpha
```

Expected: Should show "Alpha" channel present

**Step 4: Check file size**

```bash
ls -lh images/iatec_logo.png
```

Expected: File exists, reasonable size (likely 10-30KB for PNG)

---

## Task 2: Replace Logo HTML and Update CSS

**Files:**
- Modify: `index.html` (line 227 for HTML, lines 81-92 for CSS)

**Step 1: Update logo HTML**

Find (line 227):
```html
<div class="logo">iatech</div>
```

Replace with:
```html
<img src="images/iatec_logo.png" alt="iatech" class="logo">
```

**Step 2: Update logo CSS**

Find (lines 81-92):
```css
.logo {
    width: 80px;
    height: 80px;
    background: #fff;
    border-radius: 50%;
    margin-bottom: 1.5rem;
    display: flex;
    justify-content: center;
    align-items: center;
    font-weight: bold;
    color: #1a1a2e;
    font-size: 0.8rem;
}
```

Replace with:
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

**Step 3: Verify in browser**

Open `index.html` in browser:
- Expected: Logo displays as transparent PNG
- Expected: Drop shadow visible around logo
- Expected: Logo visible over video background

---

## Task 3: Add Language Toggle HTML

**Files:**
- Modify: `index.html` (add after opening `<body>` tag, around line 210)

**Step 1: Add language toggle HTML**

After the `<body>` tag (line 210), add:

```html
<body>

    <!-- Language Toggle -->
    <div class="language-toggle">
        <span class="lang-btn active" data-lang="fr">FR</span>
        <span class="separator">|</span>
        <span class="lang-btn" data-lang="en">EN</span>
        <span class="separator">|</span>
        <span class="lang-btn" data-lang="es">ES</span>
    </div>

    <!-- Navigation dots -->
```

**Step 2: Verify HTML structure**

Check that:
- Language toggle is the first element in `<body>`
- Three language buttons with correct `data-lang` attributes
- FR button has `active` class
- Separators between buttons

---

## Task 4: Add Language Toggle CSS

**Files:**
- Modify: `index.html` (add CSS in `<style>` section, around line 200)

**Step 1: Add language toggle CSS**

Add before the closing `</style>` tag (around line 200):

```css
/* Language Toggle */
.language-toggle {
    position: fixed;
    top: 1.5rem;
    right: 1.5rem;
    z-index: 200;
    background: rgba(255, 255, 255, 0.15);
    backdrop-filter: blur(10px);
    padding: 0.5rem 1rem;
    border-radius: 20px;
    display: flex;
    align-items: center;
    gap: 0.5rem;
    font-size: 0.9rem;
    font-weight: 500;
}

.lang-btn {
    cursor: pointer;
    opacity: 0.5;
    transition: opacity 0.2s, font-weight 0.2s;
    color: #fff;
}

.lang-btn:hover {
    opacity: 0.7;
}

.lang-btn.active {
    opacity: 1;
    font-weight: 700;
}

.separator {
    color: #fff;
    opacity: 0.3;
}
```

**Step 2: Verify in browser**

Open `index.html`:
- Expected: Toggle appears in top-right corner
- Expected: Frosted glass background effect
- Expected: FR is bold (active)
- Expected: EN and ES are dimmed
- Expected: Hover brightens inactive languages

---

## Task 5: Add data-lang-key Attributes to HTML

**Files:**
- Modify: `index.html` (Frame 1: line 228-229, Frame 2: line 249-250, Frame 3: line 262-263, Frame 4: line 277, 281, 284, 287)

**Step 1: Add attributes to Frame 1**

Find (lines 228-229):
```html
<h1 class="headline">L'informatique.<br>Sans bullshit.</h1>
<p class="subline">Réparation • IA • Solutions</p>
```

Replace with:
```html
<h1 class="headline" data-lang-key="frame1.headline">L'informatique.<br>Sans bullshit.</h1>
<p class="subline" data-lang-key="frame1.subline">Réparation • IA • Solutions</p>
```

**Step 2: Add attributes to Frame 2**

Find (lines 249-250):
```html
<h2 class="headline">Ça marche plus?<br>Ça va marcher.</h2>
<p class="subline">PC • Portable • Imprimante • IA</p>
```

Replace with:
```html
<h2 class="headline" data-lang-key="frame2.headline">Ça marche plus?<br>Ça va marcher.</h2>
<p class="subline" data-lang-key="frame2.subline">PC • Portable • Imprimante • IA</p>
```

**Step 3: Add attributes to Frame 3**

Find (lines 262-263):
```html
<h2 class="headline">Ton voisin<br>informatique.</h2>
<p class="subline">30 ans d'expérience • Service rapide</p>
```

Replace with:
```html
<h2 class="headline" data-lang-key="frame3.headline">Ton voisin<br>informatique.</h2>
<p class="subline" data-lang-key="frame3.subline">30 ans d'expérience • Service rapide</p>
```

**Step 4: Add attributes to Frame 4**

Find (lines 277, 281, 284, 287):
```html
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
```

Replace with:
```html
<h2 class="headline" data-lang-key="frame4.headline">On jase?</h2>

<div class="contact-content">
    <a href="tel:+1234567890" class="contact-link">
        📞 <span data-lang-key="frame4.contact1">Appelle</span>
    </a>
    <a href="mailto:info@iatechinfo.com" class="contact-link">
        ✉️ <span data-lang-key="frame4.contact2">Écris</span>
    </a>
    <a href="#" class="contact-link">
        💬 <span data-lang-key="frame4.contact3">Messenger</span>
    </a>
</div>
```

**Step 5: Verify attributes**

Check in editor:
- All headlines have `data-lang-key="frameN.headline"`
- All sublines have `data-lang-key="frameN.subline"`
- Contact spans have `data-lang-key="frame4.contactN"`

---

## Task 6: Create Translations JavaScript Object

**Files:**
- Modify: `index.html` (add to `<script>` section, before existing JavaScript, around line 297)

**Step 1: Add translations object**

Add at the top of the `<script>` section (line 297, before "Update active dot..." comment):

```javascript
// Translations
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
    en: {
        frame1: {
            headline: "Tech.<br>No bullshit.",
            subline: "Repair • AI • Solutions"
        },
        frame2: {
            headline: "Not working?<br>We'll fix it.",
            subline: "PC • Laptop • Printer • AI"
        },
        frame3: {
            headline: "Your local<br>tech.",
            subline: "30 years experience • Fast service"
        },
        frame4: {
            headline: "Let's talk?",
            contact1: "Call",
            contact2: "Write",
            contact3: "Messenger"
        }
    },
    es: {
        frame1: {
            headline: "Tecnología.<br>Sin rodeos.",
            subline: "Reparación • IA • Soluciones"
        },
        frame2: {
            headline: "¿No funciona?<br>Lo arreglamos.",
            subline: "PC • Portátil • Impresora • IA"
        },
        frame3: {
            headline: "Tu técnico<br>local.",
            subline: "30 años de experiencia • Servicio rápido"
        },
        frame4: {
            headline: "¿Hablamos?",
            contact1: "Llama",
            contact2: "Escribe",
            contact3: "Messenger"
        }
    }
};

let currentLanguage = 'fr';
```

**Step 2: Verify JavaScript syntax**

Open browser console:
- Expected: No syntax errors
- Expected: `translations` object accessible in console

---

## Task 7: Implement Language Switching JavaScript

**Files:**
- Modify: `index.html` (add to `<script>` section, after translations object)

**Step 1: Add switchLanguage function**

Add after the `currentLanguage` variable:

```javascript
// Language switching function
function switchLanguage(lang) {
    currentLanguage = lang;

    // Update all elements with data-lang-key
    document.querySelectorAll('[data-lang-key]').forEach(el => {
        const key = el.getAttribute('data-lang-key');
        const keys = key.split('.');
        const frame = keys[0];
        const field = keys[1];

        if (translations[lang] && translations[lang][frame] && translations[lang][frame][field]) {
            el.innerHTML = translations[lang][frame][field];
        }
    });

    // Update active language button
    document.querySelectorAll('.lang-btn').forEach(btn => {
        btn.classList.toggle('active', btn.dataset.lang === lang);
    });
}
```

**Step 2: Add click event listeners**

Add after the `switchLanguage` function:

```javascript
// Language toggle click handlers
document.querySelectorAll('.lang-btn').forEach(btn => {
    btn.addEventListener('click', () => {
        switchLanguage(btn.dataset.lang);
    });
});
```

**Step 3: Test in browser**

Open `index.html`:
- Click "EN" button
- Expected: All text switches to English
- Expected: EN button becomes bold
- Click "ES" button
- Expected: All text switches to Spanish
- Expected: ES button becomes bold
- Click "FR" button
- Expected: All text returns to French
- Expected: FR button becomes bold

**Step 4: Check console for errors**

Open browser console:
- Expected: No errors when clicking language buttons
- Expected: Text changes smoothly

---

## Task 8: Final Verification

**Files:**
- Verify: `index.html` (entire file)
- Verify: `images/iatec_logo.png`
- Verify: Browser console
- Verify: All 4 frames in browser

**Step 1: Full page language test**

Open `index.html` and test each language:

**French (FR):**
- Frame 1: "L'informatique. Sans bullshit." + "Réparation • IA • Solutions"
- Frame 2: "Ça marche plus? Ça va marcher." + "PC • Portable • Imprimante • IA"
- Frame 3: "Ton voisin informatique." + "30 ans d'expérience • Service rapide"
- Frame 4: "On jase?" + "Appelle" / "Écris" / "Messenger"

**English (EN):**
- Frame 1: "Tech. No bullshit." + "Repair • AI • Solutions"
- Frame 2: "Not working? We'll fix it." + "PC • Laptop • Printer • AI"
- Frame 3: "Your local tech." + "30 years experience • Fast service"
- Frame 4: "Let's talk?" + "Call" / "Write" / "Messenger"

**Spanish (ES):**
- Frame 1: "Tecnología. Sin rodeos." + "Reparación • IA • Soluciones"
- Frame 2: "¿No funciona? Lo arreglamos." + "PC • Portátil • Impresora • IA"
- Frame 3: "Tu técnico local." + "30 años de experiencia • Servicio rápido"
- Frame 4: "¿Hablamos?" + "Llama" / "Escribe" / "Messenger"

**Step 2: Logo verification**

Check Frame 1:
- ✓ Logo displays as PNG image (not circular div)
- ✓ Transparent background visible
- ✓ Drop shadow makes logo visible over video
- ✓ Logo maintains aspect ratio

**Step 3: Language toggle UI test**

- ✓ Toggle visible in top-right corner
- ✓ Frosted glass background effect
- ✓ Active language is bold and bright
- ✓ Inactive languages are dimmed (50% opacity)
- ✓ Hover on inactive languages brightens them
- ✓ Click switches language instantly
- ✓ Active state moves to clicked language

**Step 4: Responsive test**

Open browser DevTools, switch to mobile view:
- ✓ Language toggle still visible and accessible
- ✓ Logo scales appropriately
- ✓ All text readable in all languages
- ✓ No layout breaks

**Step 5: Console check**

Open browser console:
- Expected: No errors
- Expected: No warnings
- Expected: All event listeners working

**Step 6: Cross-browser test (optional)**

Test in:
- Chrome/Edge: All features work
- Firefox: All features work
- Safari: All features work (especially backdrop-filter)

---

## Success Criteria Checklist

Before marking complete, verify:

- [ ] `iatec_logo.png` exists with transparent background
- [ ] Logo displays as image (not div) with drop shadow
- [ ] Logo visible over all video backgrounds
- [ ] Language toggle appears in top-right corner
- [ ] Toggle has frosted glass effect
- [ ] FR is active by default (bold, bright)
- [ ] Clicking EN switches all text to English
- [ ] Clicking ES switches all text to Spanish
- [ ] Clicking FR switches back to French
- [ ] Active language button is bold
- [ ] Inactive languages are dimmed
- [ ] Hover brightens inactive languages
- [ ] All Frame 1 text translates (headline + subline)
- [ ] All Frame 2 text translates (headline + subline)
- [ ] All Frame 3 text translates (headline + subline)
- [ ] All Frame 4 text translates (headline + 3 contact links)
- [ ] No layout shifts when switching languages
- [ ] No console errors
- [ ] Works on mobile and desktop
- [ ] Toggle always visible when scrolling

---

## Notes for Engineer

**Logo conversion:**
- If ImageMagick not installed: `sudo apt-get install imagemagick` (Ubuntu/Debian) or `brew install imagemagick` (Mac)
- The `-fuzz 10%` handles slight variations in white color
- If logo still has white edges, increase fuzz to 15% or 20%

**Language toggle:**
- Fixed position keeps it accessible on all frames
- `backdrop-filter: blur(10px)` creates frosted glass effect (may not work in older browsers)
- z-index 200 ensures it's above videos (z-index 0) and overlay (z-index 1) and content (z-index 2)

**Translations:**
- All stored in one `translations` object for easy maintenance
- `data-lang-key` uses dot notation: `frame1.headline`
- JavaScript splits on `.` to navigate object: `translations['en']['frame1']['headline']`

**Testing:**
- Test ALL three languages on ALL four frames
- Verify location tags DON'T translate (they shouldn't have data-lang-key)
- Check that line breaks (`<br>`) are preserved in translations

**Common issues:**
- If toggle doesn't appear: Check z-index and fixed positioning
- If text doesn't switch: Check data-lang-key attributes match translations object keys
- If logo has white background: Increase -fuzz percentage in convert command
- If backdrop-filter doesn't work: Fallback is the rgba background (still looks good)
