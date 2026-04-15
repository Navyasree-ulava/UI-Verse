## ✨ Add Hamburger Menu & Sidebar Navigation Improvements

**Closes #35**

---

### 📋 Summary

This PR implements a fully responsive hamburger menu for the sidebar navigation, resolving the UX issue reported in #35. In addition to the hamburger toggle, several sidebar bugs discovered during implementation have been fixed to ensure consistent behavior across all pages.

---

### 🔧 Changes Made

#### 1. Hamburger Menu (Mobile Responsiveness)
- Added a fixed `☰` hamburger button visible on all screen sizes
- On **mobile (≤ 900px)**: toggles the sidebar open/closed with a smooth slide animation
- On **desktop**: tucked inside the sidebar header area as a subtle icon; collapses into a standalone pill button when sidebar is hidden
- Added a **semi-transparent backdrop** (`sidebar-backdrop`) on mobile that closes the sidebar on tap
- Sidebar **auto-closes on mobile** when a nav link is clicked (no more lingering open sidebar after navigation)

#### 2. Smooth Sidebar Transitions
- Sidebar slides in/out using `transform: translateX()` with `cubic-bezier` easing
- Hamburger button animates its `left` position in sync with the sidebar toggle
- Mobile sidebar uses a dark overlay backdrop with `opacity` transition for a polished feel

#### 3. Sidebar State Persistence (Desktop)
- Used `sessionStorage` to remember whether the user collapsed the sidebar
- Sidebar state is restored on every page load via `restoreSidebarState()`, preventing the jarring reset that happened on each navigation

#### 4. Active Link Fix — Case-Insensitive Matching
- `updateSidebarActiveLink()` now compares URLs **case-insensitively** (`.toLowerCase()`)
- Fixes the issue where `Navbar.html` (capital N filename) was never matched against `href="navbar.html"`, so the active highlight was missing on the Navbars page

#### 5. Fixed Broken Stub Pages (`footer.html`, `form.html`, `color.html`)
- All three pages were copy-pasted from `Navbar.html` and had:
  - Wrong `<title>` tag (all said "Navbars - UIverse")
  - Wrong hardcoded `active` class (Navbars was highlighted instead of the correct page)
  - **Missing `<main class="main">`** — this caused the layout to collapse (sidebar with no content beside it)
- Each page now has the correct title, correct active link, and a proper main content area

#### 6. Fixed Navbar.html Sidebar Link Order
- The Navbars page had its own sidebar link at the **bottom** of the list (position 7), different from every other page where it appears at position 3 (after Buttons)
- Corrected to: Home → Buttons → **Navbars** → Cards → Footer → Forms → Colors — consistent across all pages

---

### 📁 Files Changed

| File | Change |
|------|--------|
| `script.js` | Added `toggleSidebar()`, `restoreSidebarState()`, `initSidebarLinkClose()`, case-insensitive active link detection |
| `style.css` | Hamburger button styles, sidebar transition, mobile media query, backdrop overlay |
| `Navbar.html` | Fixed sidebar link order |
| `footer.html` | Fixed title, active class, added missing `<main>` |
| `form.html` | Fixed title, active class, added missing `<main>` |
| `color.html` | Fixed title, active class, added missing `<main>` |

---

### 📱 Responsive Behavior

| Screen | Sidebar Behavior |
|--------|-----------------|
| Desktop (> 900px) | Sidebar always visible; hamburger tucks inside sidebar header; can be collapsed |
| Mobile (≤ 900px) | Sidebar hidden by default; hamburger at top-left opens it with overlay backdrop |

---

### ✅ Testing Done

- [x] Sidebar opens and closes correctly on mobile
- [x] Backdrop closes sidebar on tap (mobile)
- [x] Sidebar auto-closes when a nav link is clicked (mobile)
- [x] Correct active link highlighted on every page including Navbars
- [x] Sidebar collapsed state persists across page navigations (desktop)
- [x] No layout collapse on Footer, Forms, Colors pages
- [x] Hamburger button position looks clean on both desktop and mobile
- [x] Existing desktop layout unchanged

---

### 🔗 Related Issue

Closes #35 — *Add hamburger menu for responsive sidebar navigation to improve UX*
