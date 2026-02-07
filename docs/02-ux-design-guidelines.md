# UX Design Guidelines - User Convenience Focused

A comprehensive guide for designing a user-friendly kiosk experience that prioritizes accessibility, ease of use, and customer satisfaction.

---

## Table of Contents

1. [Design Philosophy](#design-philosophy)
2. [Touch Interface Principles](#1-touch-interface-principles)
3. [Visual Design System](#2-visual-design-system)
4. [Navigation & Flow](#3-navigation--flow)
5. [Accessibility Standards](#4-accessibility-standards)
6. [Error Prevention & Handling](#5-error-prevention--handling)
7. [Performance Considerations](#6-performance-considerations)
8. [Kiosk Environment Factors](#7-kiosk-environment-factors)

---

## Design Philosophy

### Core Principles

| Principle | Description |
|-----------|-------------|
| **Simplicity First** | Every screen should have one clear purpose |
| **Forgiveness** | Users should easily recover from mistakes |
| **Consistency** | Same patterns throughout the interface |
| **Feedback** | Every action should have visible response |
| **Speed** | Minimize steps to complete an order |

### User-Centered Approach

```
     ┌─────────────────────────────────────────────┐
     │           USER CONVENIENCE PYRAMID          │
     └─────────────────────────────────────────────┘
                          /\
                         /  \
                        /    \
                       / Easy  \
                      /  to Use \
                     /────────────\
                    /   Accessible  \
                   /  to All Users   \
                  /────────────────────\
                 /    Fast & Efficient   \
                /──────────────────────────\
               /     Reliable & Stable       \
              └────────────────────────────────┘
```

---

## 1. Touch Interface Principles

### 1.1 Touch Target Sizing

**Minimum Sizes (Accessibility Standard)**

| Element Type | Minimum Size | Recommended Size |
|--------------|--------------|------------------|
| Primary Button | 44px x 44px | 60px x 60px |
| Secondary Button | 44px x 44px | 48px x 48px |
| Menu Item Card | 150px x 150px | 180px x 180px |
| Quantity Controls | 44px x 44px | 56px x 56px |
| Close/Cancel | 44px x 44px | 48px x 48px |

**Visual Example:**
```
┌──────────────────────────────────────────┐
│                                          │
│   TOO SMALL        ACCEPTABLE    IDEAL   │
│                                          │
│   ┌────┐          ┌────────┐   ┌──────┐  │
│   │ + │ (30px)    │   +    │   │  +   │  │
│   └────┘          │        │   │      │  │
│                   └────────┘   │      │  │
│                    (44px)      └──────┘  │
│                                 (60px)   │
└──────────────────────────────────────────┘
```

### 1.2 Spacing Between Touch Targets

- **Minimum spacing:** 8px between interactive elements
- **Recommended spacing:** 16px for primary actions
- **Prevents:** Accidental taps on wrong elements

```css
/* Example CSS */
.button-group {
  display: flex;
  gap: 16px; /* Adequate spacing */
}

.cart-item-controls {
  display: flex;
  gap: 12px; /* Minimum for quantity buttons */
}
```

### 1.3 Touch Feedback

**Immediate Visual Response:**

| Feedback Type | Timing | Implementation |
|---------------|--------|----------------|
| Press state | Instant | Background color change |
| Release animation | 100-200ms | Subtle scale or ripple |
| Loading state | > 300ms | Spinner or progress |
| Success confirmation | 500ms | Check mark or color |

```css
/* Touch feedback example */
.touch-button {
  transition: transform 0.1s, background-color 0.1s;
}

.touch-button:active {
  transform: scale(0.97);
  background-color: var(--primary-dark);
}
```

### 1.4 Gesture Support

| Gesture | Action | Use Case |
|---------|--------|----------|
| Single Tap | Select/Confirm | Primary interaction |
| Swipe Left | Delete item | Cart item removal |
| Swipe Down | Scroll | Menu browsing |
| Long Press | Avoid | Confusing for users |
| Pinch/Zoom | Disable | Not needed for kiosk |

---

## 2. Visual Design System

### 2.1 Color Palette

**Primary Colors:**
```css
:root {
  /* Brand Colors */
  --primary: #FF6B35;           /* Orange - Primary CTAs */
  --primary-dark: #E55A2B;      /* Darker orange - Hover/Active */
  --primary-light: #FF8C5A;     /* Lighter orange - Highlights */

  /* Neutral Colors */
  --secondary: #2E4057;         /* Dark blue - Headers */
  --background: #F7F7F7;        /* Light gray - Page background */
  --surface: #FFFFFF;           /* White - Cards, modals */

  /* Text Colors */
  --text-primary: #333333;      /* Main text */
  --text-secondary: #666666;    /* Secondary text */
  --text-disabled: #999999;     /* Disabled state */

  /* Semantic Colors */
  --success: #4CAF50;           /* Green - Confirmations */
  --warning: #FF9800;           /* Orange - Warnings */
  --danger: #F44336;            /* Red - Errors, Remove */
  --info: #2196F3;              /* Blue - Information */
}
```

**Color Contrast Requirements:**
- Text on background: Minimum 4.5:1 ratio
- Large text (18px+): Minimum 3:1 ratio
- Interactive elements: Clear visual distinction

### 2.2 Typography

**Font Scale:**
```css
:root {
  /* Font Sizes - Kiosk Optimized */
  --font-xs: 14px;      /* Legal text, timestamps */
  --font-sm: 16px;      /* Secondary info */
  --font-base: 18px;    /* Body text minimum */
  --font-lg: 22px;      /* Item names */
  --font-xl: 28px;      /* Section headers */
  --font-2xl: 36px;     /* Page titles */
  --font-3xl: 48px;     /* Order numbers */
  --font-hero: 72px;    /* Welcome screen */

  /* Font Weights */
  --font-normal: 400;
  --font-medium: 500;
  --font-semibold: 600;
  --font-bold: 700;

  /* Line Heights */
  --leading-tight: 1.2;
  --leading-normal: 1.5;
  --leading-relaxed: 1.75;
}
```

**Typography Hierarchy:**
```
┌─────────────────────────────────────────────┐
│  WELCOME TO OUR RESTAURANT    (72px, Bold)  │
│                                             │
│  Menu Categories              (28px, Semi)  │
│                                             │
│  Classic Burger               (22px, Semi)  │
│  Juicy beef patty with...     (18px, Norm)  │
│  ₩8,500                       (22px, Bold)  │
│                                             │
│  [  Add to Cart  ]            (18px, Semi)  │
└─────────────────────────────────────────────┘
```

### 2.3 Spacing System

**8px Base Unit:**
```css
:root {
  --space-1: 4px;    /* Tight spacing */
  --space-2: 8px;    /* Default small */
  --space-3: 12px;   /* Compact */
  --space-4: 16px;   /* Default medium */
  --space-5: 24px;   /* Comfortable */
  --space-6: 32px;   /* Spacious */
  --space-7: 48px;   /* Large sections */
  --space-8: 64px;   /* Page margins */
}
```

### 2.4 Component Styling

**Button Styles:**
```
Primary Button (CTA)
┌─────────────────────────────────┐
│                                 │
│   [ Add to Cart - ₩8,500 ]      │  Orange bg, white text
│                                 │   Bold, rounded corners
└─────────────────────────────────┘

Secondary Button
┌─────────────────────────────────┐
│                                 │
│   [ Back to Menu ]              │  White bg, dark text
│                                 │   Border, rounded corners
└─────────────────────────────────┘

Danger Button
┌─────────────────────────────────┐
│                                 │
│   [ Cancel Order ]              │  Red bg or red text
│                                 │   Clear warning indication
└─────────────────────────────────┘
```

**Card Styles:**
```css
.menu-item-card {
  background: var(--surface);
  border-radius: 12px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.08);
  padding: var(--space-4);
  transition: transform 0.2s, box-shadow 0.2s;
}

.menu-item-card:active {
  transform: scale(0.98);
  box-shadow: 0 1px 4px rgba(0, 0, 0, 0.12);
}
```

---

## 3. Navigation & Flow

### 3.1 Linear Flow Design

**The Golden Rule:** Users should always know where they are and how to proceed.

```
Step 1          Step 2          Step 3          Step 4
┌─────┐        ┌─────┐        ┌─────┐        ┌─────┐
│START│───────>│MENU │───────>│CHECK│───────>│DONE │
│     │        │     │        │ OUT │        │     │
└─────┘        └─────┘        └─────┘        └─────┘
                  │              │
                  │<─────────────┤ (Back option)
                  │              │
                  v              │
               ┌─────┐           │
               │ITEM │───────────┘
               │MODAL│
               └─────┘
```

### 3.2 Navigation Elements

**Progress Indicator:**
```
┌──────────────────────────────────────────────────┐
│                                                  │
│    ●───────────●───────────○───────────○         │
│   Start      Order      Checkout     Done        │
│                                                  │
└──────────────────────────────────────────────────┘
```

**Always-Visible Elements:**
| Element | Location | Purpose |
|---------|----------|---------|
| Logo | Top left | Brand identity, home link |
| Cart summary | Right side/Top right | Current order status |
| Back button | Top left or bottom | Return to previous step |
| Cancel order | Top right | Exit entire flow |

### 3.3 Modal Behavior

**Overlay Design:**
- Dark semi-transparent backdrop (50-70% opacity)
- Centered modal with white background
- Clear close button (X) in top right
- Tap outside to close (optional)

**Modal Hierarchy:**
```
┌─────────────────────────────────────────┐
│ Main Screen (dimmed)                    │
│                                         │
│    ┌───────────────────────────────┐    │
│    │         Item Detail       [X] │    │
│    │                               │    │
│    │        Modal Content          │    │
│    │                               │    │
│    │  [ Cancel ]  [ Add to Cart ]  │    │
│    └───────────────────────────────┘    │
│                                         │
└─────────────────────────────────────────┘
```

### 3.4 Transition Animations

| Transition | Duration | Easing | Use Case |
|------------|----------|--------|----------|
| Page slide | 300ms | ease-out | Screen navigation |
| Modal fade | 200ms | ease-in-out | Open/close modals |
| Cart update | 200ms | ease-out | Add/remove items |
| Button press | 100ms | ease-out | Touch feedback |

```css
/* Page transition example */
.page-enter-active,
.page-leave-active {
  transition: transform 0.3s ease-out, opacity 0.3s ease-out;
}

.page-enter-from {
  transform: translateX(100%);
  opacity: 0;
}

.page-leave-to {
  transform: translateX(-100%);
  opacity: 0;
}
```

---

## 4. Accessibility Standards

### 4.1 Visual Accessibility

**Color Blindness Considerations:**
- Never rely on color alone for information
- Use icons + color for status indicators
- Test with color blindness simulators

**Example - Status Indicators:**
```
❌ Bad:  Only color shows status
   ● (green)  ● (red)  ● (yellow)

✓ Good: Color + icon + text
   ✓ Available   ✗ Sold Out   ⚠ Low Stock
   (green)       (red)        (yellow)
```

### 4.2 Screen Reader Support

**Semantic HTML:**
```html
<!-- Use proper ARIA labels -->
<button
  aria-label="Add Classic Burger to cart, price 8,500 won"
  class="add-to-cart-btn"
>
  Add to Cart
</button>

<!-- Announce dynamic changes -->
<div
  role="status"
  aria-live="polite"
  class="cart-total"
>
  Cart total: 26,500 won
</div>
```

### 4.3 Motor Accessibility

**Large Hit Areas:**
- All interactive elements minimum 44x44px
- Generous spacing between touch targets
- Support for assistive devices

**Timeout Considerations:**
```javascript
// Session timeout with warning
const TIMEOUT_WARNING = 120000;  // 2 minutes
const TIMEOUT_EXTENSION = 60000; // 1 minute extension

function showTimeoutWarning() {
  showModal({
    title: "Are you still there?",
    message: "Your session will expire soon.",
    primaryAction: "Continue Ordering",
    secondaryAction: "Start Over"
  });
}
```

### 4.4 Cognitive Accessibility

**Simplify Information:**
- One primary action per screen
- Clear, simple language
- Visual progress indicators
- Consistent button placement

**Reading Level:**
- Target 6th-grade reading level
- Avoid jargon and technical terms
- Use familiar food terminology

---

## 5. Error Prevention & Handling

### 5.1 Prevention Strategies

**Input Validation:**
| Scenario | Prevention Method |
|----------|-------------------|
| Empty cart checkout | Disable checkout button |
| Invalid quantity | Constrain to valid range |
| Required option missing | Highlight and prompt |
| Session timeout | Warning before expiration |

**Confirmation for Destructive Actions:**
```
┌─────────────────────────────────────┐
│                                     │
│     Clear your entire cart?         │
│                                     │
│   This will remove all items        │
│   from your order.                  │
│                                     │
│   [ Cancel ]    [ Clear Cart ]      │
│                                     │
└─────────────────────────────────────┘
```

### 5.2 Error Messages

**Good Error Message Formula:**
1. What happened (clearly stated)
2. Why it happened (if helpful)
3. How to fix it (actionable)

**Examples:**
```
❌ Bad:  "Error 500"
❌ Bad:  "Something went wrong"
✓ Good: "Payment declined. Please try another card or pay at the counter."

❌ Bad:  "Invalid selection"
✓ Good: "Please select a size to continue."
```

### 5.3 Recovery Options

**Always Provide an Escape:**
- Cancel button visible on every screen
- Back navigation available
- Clear path to start over
- Help/assistance option

```
┌─────────────────────────────────────────────┐
│  Payment Failed                             │
│                                             │
│  Your card was declined.                    │
│                                             │
│  [ Try Again ]           Primary action     │
│  [ Use Different Card ]  Alternative        │
│  [ Pay at Counter ]      Alternative        │
│  [ Cancel Order ]        Exit option        │
│                                             │
└─────────────────────────────────────────────┘
```

---

## 6. Performance Considerations

### 6.1 Response Time Standards

| Action | Target Time | User Perception |
|--------|-------------|-----------------|
| Touch feedback | < 100ms | Instant |
| Page transition | < 300ms | Quick |
| Add to cart | < 500ms | Responsive |
| Data loading | < 1s | Acceptable |
| Checkout process | < 3s | Patient |

### 6.2 Loading States

**Progressive Loading:**
```
Phase 1: Skeleton screens (immediate)
┌─────────────────┐
│  ░░░░░░░░░░░░░  │
│  ░░░░░░░░░░░░░  │
│  ░░░  ₩░,░░░   │
└─────────────────┘

Phase 2: Low-res images (fast)
Phase 3: High-res images (complete)
```

**Loading Indicators:**
```css
/* Skeleton animation */
.skeleton {
  background: linear-gradient(
    90deg,
    #f0f0f0 25%,
    #e0e0e0 50%,
    #f0f0f0 75%
  );
  background-size: 200% 100%;
  animation: shimmer 1.5s infinite;
}

@keyframes shimmer {
  0% { background-position: 200% 0; }
  100% { background-position: -200% 0; }
}
```

### 6.3 Optimistic UI Updates

```javascript
// Update UI immediately, sync with server in background
async function addToCart(item) {
  // Immediate UI update
  cartStore.addItem(item);
  showSuccessToast("Added to cart!");

  // Background sync (if needed)
  try {
    await syncWithServer(cartStore.items);
  } catch (error) {
    // Rollback if sync fails
    cartStore.removeItem(item.id);
    showErrorToast("Failed to add item. Please try again.");
  }
}
```

---

## 7. Kiosk Environment Factors

### 7.1 Physical Considerations

**Screen Specifications:**
| Factor | Recommendation |
|--------|----------------|
| Screen size | 21-27 inches typical |
| Resolution | 1920x1080 (Full HD) |
| Orientation | Portrait or Landscape |
| Touch type | Capacitive (multi-touch) |
| Brightness | 300-500 nits |
| Viewing angle | 170+ degrees |

**Environmental Factors:**
```
┌─────────────────────────────────────────────┐
│  LIGHTING CONSIDERATIONS                    │
│                                             │
│  - High contrast colors for any lighting    │
│  - Anti-glare screen recommended            │
│  - Avoid pure white backgrounds in dark     │
│    environments (eye strain)                │
│                                             │
│  HEIGHT CONSIDERATIONS                      │
│                                             │
│  - Mount at 48-54 inches (center of screen) │
│  - Consider wheelchair accessibility        │
│  - Angle screen slightly downward           │
│                                             │
└─────────────────────────────────────────────┘
```

### 7.2 Session Management

**Auto-Reset Behavior:**
```javascript
const SESSION_CONFIG = {
  idleWarningTimeout: 120000,   // 2 min idle → warning
  idleResetTimeout: 30000,      // 30 sec after warning → reset
  orderCompleteReset: 30000,    // 30 sec after complete → reset

  resetActions: [
    'clearCart',
    'navigateToHome',
    'clearLocalStorage',
    'resetLanguage'
  ]
};
```

**Session States:**
```
┌─────────────────────────────────────────────────────────┐
│  Session Lifecycle                                      │
│                                                         │
│  IDLE ──> ACTIVE ──> ORDERING ──> CHECKOUT ──> COMPLETE │
│    │                                              │     │
│    └──────────────── TIMEOUT ◄────────────────────┘     │
│                         │                               │
│                         v                               │
│                       RESET                             │
└─────────────────────────────────────────────────────────┘
```

### 7.3 Offline Capability

**Graceful Degradation:**
```javascript
// Handle network issues
if (!navigator.onLine) {
  showBanner({
    type: 'warning',
    message: 'Internet connection lost. Some features may be unavailable.',
    persistent: true
  });

  // Fall back to cached menu
  menuStore.loadFromCache();

  // Disable features requiring network
  disableFeatures(['payment', 'receipt-email']);
}
```

### 7.4 Screen Resolution Handling

**Fixed Viewport Design:**
```css
/* Lock viewport to prevent zoom */
html {
  touch-action: manipulation;
  -webkit-text-size-adjust: 100%;
}

/* Fixed dimensions for kiosk screen */
.kiosk-app {
  width: 1080px;  /* or your target width */
  height: 1920px; /* portrait mode */
  overflow: hidden;
  position: fixed;
  top: 0;
  left: 0;
}
```

---

## Quick Reference Checklist

### Before Launch Verification

- [ ] All touch targets are minimum 44x44px
- [ ] Color contrast ratios meet WCAG AA (4.5:1)
- [ ] Text is minimum 18px for body content
- [ ] Every action has visual feedback
- [ ] Error messages are clear and actionable
- [ ] Navigation flow is linear and simple
- [ ] Session timeout warnings are implemented
- [ ] Offline fallback is functional
- [ ] Screen reader labels are complete
- [ ] Performance meets target times

---

*Document Version: 1.0*
*Last Updated: 2026-01-29*
