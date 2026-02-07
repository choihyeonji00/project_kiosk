# Key Features - Food Ordering Kiosk

A comprehensive guide to the core features and functionality of the kiosk application.

---

## Table of Contents

1. [Overview](#overview)
2. [Welcome Screen](#1-welcome-screen)
3. [Menu Browsing System](#2-menu-browsing-system)
4. [Item Customization](#3-item-customization)
5. [Shopping Cart](#4-shopping-cart)
6. [Checkout Process](#5-checkout-process)
7. [Order Confirmation](#6-order-confirmation)
8. [Feature Summary Matrix](#feature-summary-matrix)

---

## Overview

The Food Ordering Kiosk is a self-service touch interface designed for restaurant environments. It enables customers to browse menus, customize orders, and complete purchases without staff assistance.

### Core Value Proposition

| Benefit | Description |
|---------|-------------|
| **Speed** | Reduce ordering time by 40-60% compared to counter service |
| **Accuracy** | Eliminate order miscommunication errors |
| **Upselling** | Visual menus encourage add-ons and larger sizes |
| **Efficiency** | Free staff for food preparation and customer service |

---

## 1. Welcome Screen

### Purpose
The entry point that invites customers to begin their ordering journey.

### Features

#### 1.1 Start Order Button
- Large, prominent call-to-action button
- Touch-responsive with visual feedback
- Clear "Start Order" or "Order Here" text

#### 1.2 Branding Display
- Restaurant logo prominently displayed
- Brand colors and imagery
- Welcoming message or tagline

#### 1.3 Language Selection (Optional)
- Support for multiple languages
- Flag icons or language names
- Persists throughout the session

#### 1.4 Order Type Selection
```
┌─────────────────────────────────────┐
│                                     │
│         [Restaurant Logo]           │
│                                     │
│     Welcome to [Restaurant Name]    │
│                                     │
│   ┌─────────────┐ ┌─────────────┐   │
│   │   Dine In   │ │  Takeout    │   │
│   └─────────────┘ └─────────────┘   │
│                                     │
│       [ Touch to Start Order ]      │
│                                     │
└─────────────────────────────────────┘
```

### Technical Implementation
- **Route:** `/` (HomeView.vue)
- **State:** Initializes empty cart on navigation
- **Navigation:** Proceeds to `/menu` on start

---

## 2. Menu Browsing System

### Purpose
Enable customers to discover and explore available menu items efficiently.

### Features

#### 2.1 Category Navigation

**Sidebar Category List**
- Visual icons for each category
- Active category highlighting
- Smooth scroll for many categories

**Categories Example:**
| Icon | Category | Items Count |
|------|----------|-------------|
| 🍔 | Burgers | 8 items |
| 🍕 | Pizza | 6 items |
| 🍟 | Sides | 10 items |
| 🥤 | Drinks | 12 items |
| 🍰 | Desserts | 5 items |

#### 2.2 Menu Item Grid

**Grid Layout Features:**
- Responsive grid (3-4 items per row)
- High-quality item images
- Clear pricing display
- Quick-add button

**Item Card Structure:**
```
┌─────────────────┐
│   [Item Image]  │
│                 │
│  Classic Burger │
│     ₩8,500      │
│                 │
│   [ + Add ]     │
└─────────────────┘
```

#### 2.3 Search & Filter (Advanced)
- Search by item name
- Filter by dietary restrictions
- Sort by price or popularity

### Technical Implementation
- **Route:** `/menu` (MenuView.vue)
- **State:** `menu.js` Pinia store
- **Components:** CategoryList.vue, MenuGrid.vue, MenuItem.vue

---

## 3. Item Customization

### Purpose
Allow customers to personalize their orders with options and modifications.

### Features

#### 3.1 Detail Modal

When an item is selected, a modal displays:
- Larger item image
- Full description
- Nutritional info (optional)
- Customization options
- Quantity selector
- Total price calculator

#### 3.2 Option Types

**Single Selection (Required)**
```javascript
{
  name: "Size",
  required: true,
  choices: [
    { label: "Regular", price: 0 },
    { label: "Large", price: 2000 }
  ]
}
```

**Multiple Selection (Optional)**
```javascript
{
  name: "Add-ons",
  multiple: true,
  choices: [
    { label: "Extra Cheese", price: 1000 },
    { label: "Bacon", price: 1500 },
    { label: "Avocado", price: 2000 }
  ]
}
```

#### 3.3 Real-time Price Updates

The modal shows live price calculation:
```
Base Price:      ₩8,500
+ Large Size:    ₩2,000
+ Extra Cheese:  ₩1,000
─────────────────────────
Total:           ₩11,500
```

#### 3.4 Quantity Selection
- Minus (-) and Plus (+) buttons
- Minimum quantity: 1
- Maximum quantity: 10 (configurable)

### Modal Layout
```
┌─────────────────────────────────────┐
│  [X]                    Item Detail │
├─────────────────────────────────────┤
│                                     │
│          [Large Item Image]         │
│                                     │
│  Classic Burger              ₩8,500 │
│  Juicy beef patty with fresh        │
│  vegetables and special sauce       │
│                                     │
├─────────────────────────────────────┤
│  Size (Required)                    │
│  ○ Regular (+₩0)  ● Large (+₩2,000) │
│                                     │
│  Add-ons (Optional)                 │
│  ☑ Extra Cheese (+₩1,000)           │
│  ☐ Bacon (+₩1,500)                  │
│  ☐ Avocado (+₩2,000)                │
│                                     │
├─────────────────────────────────────┤
│  Quantity:  [ - ]  2  [ + ]         │
│                                     │
│  [ Add to Cart - ₩23,000 ]          │
└─────────────────────────────────────┘
```

### Technical Implementation
- **Component:** MenuItemDetail.vue
- **State:** Local component state for selections
- **Event:** Emits to cart store on add

---

## 4. Shopping Cart

### Purpose
Display and manage selected items before checkout.

### Features

#### 4.1 Cart Sidebar (Always Visible)

**Location:** Right side of menu screen
**Contents:**
- List of added items
- Item quantities
- Running total
- Checkout button

#### 4.2 Cart Item Display

Each item shows:
- Item name
- Selected options
- Quantity with +/- controls
- Item total price
- Remove button

#### 4.3 Cart Actions

| Action | UI Element | Behavior |
|--------|------------|----------|
| Increase Qty | [+] button | Increment by 1 |
| Decrease Qty | [-] button | Decrement by 1 (min: 1) |
| Remove Item | [X] or Trash icon | Remove from cart |
| Clear All | "Clear Cart" link | Empty entire cart |

#### 4.4 Cart Summary

```
┌─────────────────────────────┐
│  Your Order                 │
├─────────────────────────────┤
│  Classic Burger (Large)     │
│  + Extra Cheese             │
│  [-] 2 [+]          ₩23,000 │
│                         [X] │
├─────────────────────────────┤
│  French Fries               │
│  [-] 1 [+]           ₩3,500 │
│                         [X] │
├─────────────────────────────┤
│  Subtotal:          ₩26,500 │
│  Tax (10%):          ₩2,650 │
│  ─────────────────────────  │
│  Total:             ₩29,150 │
│                             │
│  [ Proceed to Checkout ]    │
└─────────────────────────────┘
```

#### 4.5 Empty Cart State
- Friendly message: "Your cart is empty"
- Suggestion to browse menu
- Visual illustration

### Technical Implementation
- **Components:** CartSidebar.vue, CartItem.vue, CartSummary.vue
- **State:** `cart.js` Pinia store
- **Persistence:** Optional localStorage backup

---

## 5. Checkout Process

### Purpose
Review order and complete payment.

### Features

#### 5.1 Order Review

Full-screen view of cart contents:
- All items with details
- Final price breakdown
- Ability to make last-minute changes

#### 5.2 Order Type Confirmation
- Dine-in vs Takeout reminder
- Table number input (for dine-in)

#### 5.3 Payment Methods

| Method | Implementation |
|--------|----------------|
| Card (Credit/Debit) | Hardware integration |
| Mobile Pay | QR code or NFC |
| Cash | Directs to counter |

#### 5.4 Payment Flow (Simplified)
```
┌─────────────────────────────────────┐
│         Review Your Order           │
├─────────────────────────────────────┤
│                                     │
│  2x Classic Burger (Large)  ₩23,000 │
│     + Extra Cheese                  │
│  1x French Fries             ₩3,500 │
│                                     │
│  ───────────────────────────────    │
│  Subtotal:              ₩26,500     │
│  Tax:                    ₩2,650     │
│  Total:                 ₩29,150     │
│                                     │
├─────────────────────────────────────┤
│  Select Payment Method              │
│                                     │
│  [ Credit Card ]  [ Mobile Pay ]    │
│                                     │
│        [ Pay at Counter ]           │
│                                     │
├─────────────────────────────────────┤
│  [ Back to Menu ]  [ Confirm Order ]│
└─────────────────────────────────────┘
```

#### 5.5 Validation
- Minimum order amount check
- Payment confirmation before processing
- Error handling for failed payments

### Technical Implementation
- **Route:** `/checkout` (CheckoutView.vue)
- **State:** Reads from cart store
- **Navigation:** Back to menu or forward to complete

---

## 6. Order Confirmation

### Purpose
Confirm successful order and provide pickup information.

### Features

#### 6.1 Order Number Display

Large, prominent order number:
```
┌─────────────────────────────────────┐
│                                     │
│           Order Complete!           │
│                                     │
│        Your Order Number Is         │
│                                     │
│              #042                   │
│           (Very Large)              │
│                                     │
│   Please wait for your number to    │
│   be called at the pickup counter   │
│                                     │
│   Estimated Wait: ~5 minutes        │
│                                     │
│        [ Start New Order ]          │
│                                     │
└─────────────────────────────────────┘
```

#### 6.2 Order Details
- Summary of ordered items
- Total amount paid
- Order timestamp
- Receipt option (print/email)

#### 6.3 Wait Time Estimate
- Based on current queue
- Dynamic updates (advanced)

#### 6.4 New Order Button
- Clears session
- Returns to welcome screen
- Auto-redirect after timeout (optional)

### Technical Implementation
- **Route:** `/complete` (CompleteView.vue)
- **State:** Order number from cart store
- **Cleanup:** Cart cleared after display

---

## Feature Summary Matrix

| Feature | Priority | Status | Notes |
|---------|----------|--------|-------|
| Welcome Screen | High | Planned | Entry point |
| Category Navigation | High | Planned | Core feature |
| Menu Grid Display | High | Planned | Core feature |
| Item Detail Modal | High | Planned | Core feature |
| Cart Sidebar | High | Planned | Core feature |
| Quantity Controls | High | Planned | Cart management |
| Price Calculator | High | Planned | Real-time updates |
| Checkout Review | High | Planned | Order finalization |
| Order Confirmation | High | Planned | Completion flow |
| Multiple Languages | Medium | Future | i18n support |
| Payment Integration | Medium | Future | Hardware dependent |
| Receipt Printing | Low | Future | Hardware dependent |
| Loyalty Program | Low | Future | Backend integration |

---

## User Flow Diagram

```
┌─────────┐     ┌──────────────┐     ┌─────────────┐     ┌───────────┐
│  Start  │────>│ Browse Menu  │────>│  Checkout   │────>│ Complete  │
│  Order  │     │ Add to Cart  │     │  & Pay      │     │  Order    │
└─────────┘     └──────────────┘     └─────────────┘     └───────────┘
                       │                    │                   │
                       │                    │                   │
                       v                    v                   v
                  ┌─────────┐         ┌─────────┐         ┌─────────┐
                  │  Item   │         │  Back   │         │   New   │
                  │ Detail  │         │ to Menu │         │  Order  │
                  └─────────┘         └─────────┘         └─────────┘
```

---

*Document Version: 1.0*
*Last Updated: 2026-01-29*
