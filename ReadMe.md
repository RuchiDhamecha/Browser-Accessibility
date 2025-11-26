# Accessibility in React --- Quick Practical Notes

Accessibility helps **visually impaired**, **hearing impaired**, and
**mobility impaired** users.
React + semantic HTML + ARIA = **Inclusive UI**.

------------------------------------------------------------------------

## 🔵 1. Semantic HTML First

-   Use real elements: `<button>`, `<nav>`, `<main>`, `<section>`,
    `<ul>`, `<table>`.
-   Avoid using `<div>` for interactive behavior.
-   Use `<label htmlFor="id">` for every form element.

------------------------------------------------------------------------

## 🔵 2. ARIA Essentials

Use ARIA only when HTML can't express intent.

### **ARIA Live Regions**

Used to announce dynamic content to screen readers.

  Value           Meaning
  --------------- ----------------------------------------------------
  **off**         Do not announce updates
  **polite**      Announce updates when idle
  **assertive**   Interrupt and announce immediately (use sparingly)

**Example**

``` html
<div aria-live="polite">Saving…</div>
```

------------------------------------------------------------------------

## 🔵 3. Common ARIA Attributes

-   `aria-label="Close"` → for icon buttons
-   `aria-hidden="true"` → hide decorative icons
-   `aria-describedby="error-id"` → associate error or helper text
-   `role="dialog"` → modals
-   `role="alert"` → urgent error messages

------------------------------------------------------------------------

## 🔵 4. Keyboard Accessibility

-   All interactive elements must be reachable via **Tab**.
-   **Enter** and **Space** should activate buttons/links.

### tabIndex

-   `tabIndex={0}` → focusable
-   `tabIndex={-1}` → focusable **only programmatically**

### autoFocus

Use carefully --- it may move focus unexpectedly.
Safe for dialogs & first input.

``` html
<input autoFocus />
```

------------------------------------------------------------------------

## 🔵 5. Focus Management

-   Modals should **trap focus** inside.
-   After closing modal, return focus to the original trigger.
-   MUI Dialog already manages this correctly.

------------------------------------------------------------------------

## 🔵 6. Images & Icons

-   Always add `alt="..."` text.
-   Decorative icons → `aria-hidden="true"`.

------------------------------------------------------------------------

## 🔵 7. DevTools → Rendering Tab (For A11y Debugging)

Chrome DevTools → Rendering → Enable:

-   Emulate vision deficiencies (blurred, color blindness)
-   Highlight focus (shows moving focus)
-   Helps debug keyboard accessibility + visual contrast

------------------------------------------------------------------------

## 🔵 8. Forms

Use `htmlFor="id"` on labels.
Link helper/error text with `aria-describedby`.

``` html
<label htmlFor="email">Email</label>
<input id="email" aria-describedby="email-help" />
<small id="email-help">We'll not share your email.</small>
```

------------------------------------------------------------------------

# 🟣 Accessibility for Different Impairments
## 👁️ Visually Impaired Users

-   Semantic HTML
-   ARIA live regions
-   Proper labels + alt text
-   Correct focus order
-   High contrast text
-   Keyboard-friendly UI

## 🎧 Hearing Impaired Users

-   Provide **captions/subtitles** in videos
-   Add **transcripts** for audio
-   Avoid audio-only feedback; provide visual alternative

## 🖐 Mobility Impaired Users

-   Tap target sizes ≥ **44px × 44px**
-   Adequate padding/margins
-   Avoid fast-disappearing UI
-   Support keyboard & alternative inputs

------------------------------------------------------------------------

# 🟢 Additional Smart Accessibility Tips

-   Add a **Skip to main content** link
-   Maintain heading order (`h1 → h2 → h3`)
-   Don't rely on color alone
-   Keep consistent focus styles
-   Use `prefers-reduced-motion` for reduced animations

------------------------------------------------------------------------

## WAVE Tool (Very Short)

The **WAVE Accessibility Tool** (browser extension / website) is useful for quickly validating accessibility issues, especially those affecting **visually impaired users**.

WAVE helps detect:

- Missing or incorrect labels
- Missing `alt` text on images
- Low contrast text (very important for visually impaired users)
- Incorrect heading structure
- Missing form associations (label → input)
- Landmark issues (missing `<main>`, `<nav>`, `<header>` etc.)
- ARIA misuse

Use WAVE along with **Chrome DevTools → Rendering → Vision Deficiencies** for a complete accessibility check.
