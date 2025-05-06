# Keboola Design System Component Guide

This guide provides detailed instructions on how to correctly implement components from the Keboola Design System.

## Table of Contents

1. [Getting Started](#getting-started)
   - [Installation](#installation)
   - [Basic Page Structure](#basic-page-structure)
   - [Design Tokens](#design-tokens)
     - [Color System](#color-system)
     - [Typography System](#typography-system)
     - [Spacing System](#spacing-system)
2. [Core Components](#core-components)
   - [Button Components](#button-components)
     - [Required Structure](#required-structure)
     - [Class Combinations](#class-combinations)
     - [HTML Structure](#html-structure)
       - [Text Button](#text-button)
       - [Icon + Text Button](#icon--text-button)
       - [Icon-Only Button](#icon-only-button)
     - [Common Button Mistakes](#common-button-mistakes)
   - [Form Components](#form-components)
     - [Text Input](#text-input)
       - [Required Structure](#required-structure-1)
     - [Select Input](#select-input)
       - [Required Structure](#required-structure-2)
     - [Checkbox](#checkbox)
       - [Required Structure](#required-structure-3)
     - [Radio Button](#radio-button)
       - [Required Structure](#required-structure-4)
     - [Form Validation](#form-validation)
   - [Layout Components](#layout-components)
     - [Header](#header)
     - [Grid System](#grid-system)
   - [Card Components](#card-components)
     - [Basic Card](#basic-card)
     - [Overview Card](#overview-card)
     - [Grey Overview Card](#grey-overview-card)
       - [Common Usage Pattern: Grey Overview Cards in White Container](#common-usage-pattern-grey-overview-cards-in-white-container)
     - [Card Variants](#card-variants)
     - [Card Layout Helper Classes](#card-layout-helper-classes)
   - [Activity Row](#activity-row)
   - [Tabs](#tabs)
     - [Tab Component Requirements](#tab-component-requirements)
   - [Badges](#badges)
     - [Standard Variants](#standard-variants)
     - [Inline Badge Variant](#inline-badge-variant)
     - [Using Badges as Labels or Tags](#using-badges-as-labels-or-tags)
     - [Custom Color Badges](#custom-color-badges)
     - [Badges with Icons](#badges-with-icons)
   - [Banners](#banners)
     - [Key Implementation Details](#key-implementation-details)
     - [Banner Variants](#banner-variants)
   - [Icons](#icons)
     - [Icon Sizes](#icon-sizes)
     - [Icon Colors](#icon-colors)
     - [Implementation Notes](#implementation-notes)
3. [Common Patterns](#common-patterns)
   - [Form Card Pattern](#form-card-pattern)
   - [Activity List Pattern](#activity-list-pattern)
4. [Typography Guidelines](#typography-guidelines)
   - [Typography in Components](#typography-in-components)
5. [Banner Placement Guidelines](#banner-placement-guidelines)
   - [Page-Level Banners](#page-level-banners)
   - [Card-Level Banners](#card-level-banners)
6. [Best Practices and Common Mistakes](#best-practices-and-common-mistakes)
   - [General Component Mistakes](#general-component-mistakes)
   - [Specific Component Issues](#specific-component-issues)
   - [Typography Best Practices](#typography-best-practices)
   - [Layout Best Practices](#layout-best-practices)
   - [Spacing Best Practices](#spacing-best-practices)
7. [Responsive Grid Layouts](#responsive-grid-layouts)
   - [Responsive Grid Classes](#responsive-grid-classes)
   - [Breakpoints](#breakpoints)
   - [Balanced Layouts for Uneven Numbers](#balanced-layouts-for-uneven-numbers)
     - [For 5 KPI Cards with `grid-5-cards` class](#for-5-kpi-cards-with-grid-5-cards-class)
     - [For 3 KPI Cards with `grid-3-cards` class](#for-3-kpi-cards-with-grid-3-cards-class)
   - [Example Implementation](#example-implementation)
   - [Fixed vs Responsive Grid](#fixed-vs-responsive-grid)
8. [Navigation Component](#navigation-component)
   - [Required Structure](#required-structure-5)
   - [HTML Implementation](#html-implementation)
   - [CSS Variables](#css-variables)
   - [Interactive Elements](#interactive-elements)
   - [Responsive Behavior](#responsive-behavior)
   - [Important Implementation Notes](#important-implementation-notes)
9. [Icon Component](#icon-component)
   - [Icon Sizes](#icon-sizes-1)
   - [Implementation](#implementation)
   - [Best Practices](#best-practices)
10. [Topbar Component](#topbar-component)
    - [Logo Implementation](#logo-implementation)
    - [Avatar Implementation](#avatar-implementation)
    - [Full Topbar Structure](#full-topbar-structure)
    - [Typography Classes](#typography-classes)
11. [Asset Requirements](#asset-requirements)
    - [Required Assets Structure](#required-assets-structure)
    - [Logo Usage Guidelines](#logo-usage-guidelines)
    - [Avatar Guidelines](#avatar-guidelines)
12. [Support & Contributing](#support--contributing)
    - [Support & Documentation](#support--documentation)
    - [Contributing](#contributing)

## Getting Started

### Installation

Include these dependencies in your HTML file:

```html
<!-- Required Dependencies -->
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
<link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.1/css/all.min.css" rel="stylesheet">
<link href="dist/design-system.css" rel="stylesheet">
```

### Basic Page Structure

Every page should follow this basic structure:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Keboola App</title>
    
    <!-- Preload critical fonts for performance -->
    <link rel="preload" href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" as="style">
    
    <!-- Required Dependencies -->
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.1/css/all.min.css" rel="stylesheet">
    <link href="dist/design-system.css" rel="stylesheet">
    
    <!-- REQUIRED: Base font styles -->
    <style>
        body {
            margin: 0;
            padding: 0;
            font-family: var(--font-family-base);
            background-color: var(--neutral-grey-50);
            color: var(--neutral-grey-800);
            line-height: var(--body-body-line-height);
        }
    </style>
</head>
<body class="bg-grey-50">
    <div class="container page-container" style="padding: var(--space-16)">
        <div class="content-wrapper" style="display: flex; flex-direction: column; gap: var(--space-6)">
            <header class="header">
                <h1 class="header__title heading-1">Page Title</h1>
            </header>
            
            <section class="section">
                <!-- Content -->
            </section>
        </div>
    </div>
</body>
</html>
```

> ⚠️ **Important**: Both the font preloading and base font styles are required for all pages. Omitting either will result in inconsistent typography and performance issues.

### Design Tokens

#### Color System

The design system provides a comprehensive set of color tokens:

```css
/* Neutral Colors */
--neutral-white: #ffffff;
--neutral-grey-50: #f2f4f7;    /* Background color */
--neutral-grey-100: #edf0f5;
--neutral-grey-150: #d9dde5;
--neutral-grey-200: #c5cbd6;
--neutral-grey-300: #a2aab8;
--neutral-grey-400: #7c8594;
--neutral-grey-500-base: #565c66;
--neutral-grey-600: #454952;   /* Meta text */
--neutral-grey-800: #222529;   /* Body text */
--neutral-grey-900: #101114;   /* Headings */

/* Secondary Colors - Blue */
--secondary-blue-800: #064a8f;
--secondary-blue-700: #075fb8;
--secondary-blue-600: #0975e0;  /* Primary blue for icons and accents */
--secondary-blue-500-base: #1f8fff;
--secondary-blue-450: #3e9eff;
--secondary-blue-200: #c2e0ff;
--secondary-blue-100: #e0f0ff;

/* Success Colors - Green */
--success-green-800: #158b15;
--success-green-700: #189f18;
--success-green-600: #1bb31b;
--success-green-500-base: #1ec71e;
--success-green-200: #baf5ba;
--success-green-100: #e0ffe0;

/* Warning Colors - Orange */
--warning-orange-600: #d17d00;
--warning-orange-550: #e38800;
--warning-orange-500-base: #f59300;
--warning-orange-300: #ffd699;
--warning-orange-200: #ffe7c2;
--warning-orange-100: #fff3e0;

/* Error Colors - Red */
--error-red-700: #a3001b;
--error-red-600: #b8001f;
--error-red-550: #c40021;
--error-red-500-base: #e00025;
--error-red-200: #ffc2cc;
--error-red-100: #ffe0e6;

/* Accent Colors */
--accent-purple-600: #6f36e0;
--accent-purple-500-base: #925cff;
--accent-purple-200: #d6c2ff;
--accent-purple-100: #ebe0ff;
--accent-cyan-600: #00a0b2;
--accent-cyan-500-base: #00bbd1;
--accent-cyan-200: #bef3ff;
--accent-cyan-100: #e0f9ff;
--accent-teal-600: #00a673;
--accent-teal-500-base: #00c287;
--accent-teal-200: #96ffce;
--accent-teal-100: #cfffe6;
```

#### Typography System

The design system provides consistent typography classes:

```html
<!-- Headings -->
<h1 class="heading-1">32px, Medium (500)</h1>
<h2 class="heading-2">24px, Medium (500)</h2>
<h3 class="heading-3">16px, Medium (500)</h3>
<h4 class="heading-4">12px, Medium (500)</h4>

<!-- Body Text -->
<p class="body-text">14px, Regular (400)</p>
<p class="body-text-medium">14px, Medium (500)</p>

<!-- Small Text -->
<p class="small-body-text">12px, Regular (400)</p>
<p class="small-body-text-medium">12px, Medium (500)</p>
```

#### Spacing System

The design system uses a consistent spacing scale:

```css
--space-0: 0;
--space-1: 4px;
--space-2: 8px;
--space-3: 12px;
--space-4: 16px;
--space-5: 20px;
--space-6: 24px;
--space-8: 32px;
--space-10: 40px;
--space-12: 48px;
--space-16: 64px;
```

## Core Components

### Button Components

#### Required Structure

All buttons in the Keboola Design System follow this class structure:

```
Base Class + Style Variant + Size + Optional Modifiers
```

#### Class Combinations

| Component Type | Required Classes | Example |
|----------------|------------------|---------|
| Text Button | `btn` + (`btn-primary` or `btn-secondary`) + (`btn-medium` or `btn-small`) | `<button class="btn btn-primary btn-medium">` |
| Icon + Text Button | `btn` + (`btn-primary` or `btn-secondary`) + (`btn-medium` or `btn-small`) | `<button class="btn btn-primary btn-medium">` |
| Icon-Only Button | `btn` + (`btn-primary` or `btn-secondary`) + `btn-icon-only` + (`btn-medium` or `btn-small`) | `<button class="btn btn-primary btn-icon-only btn-medium">` |

#### HTML Structure

##### Text Button

```html
<button class="btn btn-primary btn-medium">
  <span class="btn-text">BUTTON TEXT</span>
</button>
```

##### Icon + Text Button

```html
<button class="btn btn-primary btn-medium">
  <div class="btn-icon">
    <i class="fas fa-plus text-white"></i>
  </div>
  <span class="btn-text">BUTTON TEXT</span>
</button>
```

##### Icon-Only Button

```html
<button class="btn btn-primary btn-icon-only btn-medium">
  <div class="btn-icon">
    <i class="fas fa-plus text-white"></i>
  </div>
</button>
```

#### Common Button Mistakes

❌ **Missing style variant**
```html
<button class="btn btn-medium">
  <span class="btn-text">BUTTON TEXT</span>
</button>
```

❌ **Missing size class**
```html
<button class="btn btn-primary">
  <span class="btn-text">BUTTON TEXT</span>
</button>
```

❌ **Missing btn-icon wrapper**
```html
<button class="btn btn-primary btn-medium">
  <i class="fas fa-plus"></i>
  <span class="btn-text">BUTTON TEXT</span>
</button>
```

❌ **Missing btn-text wrapper**
```html
<button class="btn btn-primary btn-medium">
  BUTTON TEXT
</button>
```

❌ **Icon-only button missing style variant**
```html
<button class="btn btn-icon-only btn-medium">
  <div class="btn-icon">
    <i class="fas fa-plus"></i>
  </div>
</button>
```

### Form Components

#### Text Input

##### Required Structure

```html
<div class="form-group">
  <div class="text-input">
    <div class="label">
      <label class="label-text" for="input-id">Label Text</label>
    </div>
    <div class="content">
      <input type="text" id="input-id" placeholder="Placeholder text">
    </div>
  </div>
</div>
```

#### Select Input

##### Required Structure

```html
<div class="form-group">
  <div class="select">
    <div class="label">
      <label class="label-text" for="select-id">Label Text</label>
    </div>
    <div class="select-wrapper">
      <select id="select-id" class="select-trigger">
        <option value="">Select an option</option>
        <option value="option1">Option 1</option>
        <option value="option2">Option 2</option>
      </select>
    </div>
  </div>
</div>
```

#### Checkbox

##### Required Structure

```html
<div class="form-group">
  <label class="checkbox">
    <input type="checkbox" id="checkbox-id">
    <div class="checkbox-box"></div>
    <div class="checkbox-label">
      <span class="checkbox-label-text">Checkbox Label</span>
    </div>
  </label>
</div>
```

#### Radio Button

##### Required Structure

```html
<div class="form-group">
  <label class="radio">
    <input type="radio" name="radio-group" value="option1">
    <div class="radio-circle"></div>
    <div class="radio-label">
      <span class="radio-label-text">Radio Label</span>
    </div>
  </label>
</div>
```

#### Form Validation

```html
<!-- Error State -->
<div class="form-group">
  <div class="text-input error">
    <div class="label">
      <label class="label-text" for="error-input">Input with Error</label>
    </div>
    <div class="content">
      <input type="text" id="error-input" placeholder="Error field">
    </div>
    <div class="error-message">
      This field is required
    </div>
  </div>
</div>

<!-- Success State -->
<div class="form-group">
  <div class="text-input success">
    <div class="label">
      <label class="label-text" for="success-input">Valid Input</label>
    </div>
    <div class="content">
      <input type="text" id="success-input" value="Correct value">
    </div>
  </div>
</div>
```

### Layout Components

#### Header

```html
<header class="header">
  <h1 class="header__title">Page Title</h1>
  <div class="header__actions">
    <!-- Secondary buttons first -->
    <button class="btn btn-secondary btn-medium">
      <div class="btn-icon">
        <i class="fas fa-cog icon-muted"></i>
      </div>
      <span class="btn-text">SETTINGS</span>
    </button>
    <!-- Primary button last -->
    <button class="btn btn-primary btn-medium">
      <div class="btn-icon">
        <i class="fas fa-plus text-white"></i>
      </div>
      <span class="btn-text">ADD NEW</span>
    </button>
  </div>
</header>
```

#### Grid System

```html
<div style="display: grid; grid-template-columns: repeat(3, 1fr); gap: var(--space-4);">
  <!-- Grid items -->
</div>
```

### Card Components

#### Basic Card

```html
<div class="card bg-white">
  <h2 class="card__title">Card Title</h2>
  <div class="card__content">
    <!-- Card content goes here -->
  </div>
  <div class="card__footer">
    <!-- Footer content goes here -->
  </div>
</div>
```

#### Overview Card

```html
<div class="overview-card bg-white">
  <div class="overview-card__header">
    <span class="overview-card__title">Title</span>
    <span class="badge badge-success">
      <span class="badge-text">Status</span>
    </span>
  </div>
  <div class="overview-card__value">Value</div>
  <div class="overview-card__subtitle">Subtitle</div>
</div>
```

#### Grey Overview Card

The grey overview card variant (`overview-card--grey`) is designed to be used on white backgrounds, typically inside white cards or containers. This creates visual hierarchy and helps group related metrics.

```html
<div class="overview-card overview-card--grey">
  <div class="overview-card__header">
    <span class="overview-card__title">Title</span>
  </div>
  <div class="overview-card__value">Value</div>
  <div class="overview-card__subtitle">Subtitle</div>
</div>
```

##### Common Usage Pattern: Grey Overview Cards in White Container

A common pattern is to place multiple grey overview cards in a grid inside a white card:

```html
<!-- White container card with grey overview cards -->
<div class="card bg-white">
  <h2 class="card__title">Metrics Overview</h2>
  <div class="card__content">
    <div class="grid grid-cols-3" style="gap: var(--space-4)">
      <div class="overview-card overview-card--grey">
        <div class="overview-card__header">
          <span class="overview-card__title">Revenue</span>
        </div>
        <div class="overview-card__value">$45,678</div>
        <div class="overview-card__subtitle">This month</div>
      </div>
      
      <div class="overview-card overview-card--grey">
        <div class="overview-card__header">
          <span class="overview-card__title">Users</span>
        </div>
        <div class="overview-card__value">1,234</div>
        <div class="overview-card__subtitle">Active users</div>
      </div>
      
      <div class="overview-card overview-card--grey">
        <div class="overview-card__header">
          <span class="overview-card__title">Conversion</span>
        </div>
        <div class="overview-card__value">12.5%</div>
        <div class="overview-card__subtitle">+2.4% from last month</div>
      </div>
    </div>
  </div>
</div>
```

> ⚠️ **Important**: Always use the grey overview card variant on white backgrounds (like inside a white card). Using it directly on the page's grey background (`bg-grey-50`) will result in poor contrast and visual confusion.

#### Card Variants

```html
<!-- Card with Description -->
<div class="card card--with-description bg-white">
  <h2 class="card__title">Card Title</h2>
  <div class="card__content">
    <p class="body-text">This is a description paragraph.</p>
  </div>
</div>

<!-- Card with Icon Title -->
<div class="card bg-white">
  <div class="card__title--with-icon">
    <div class="icon-container icon-small">
      <i class="fas fa-chart-line"></i>
    </div>
    <span class="card__title-text">Card Title with Icon</span>
  </div>
  <div class="card__content">
    <!-- Content -->
  </div>
</div>
```

#### Card Layout Helper Classes

```html
<!-- Equal height cards -->
<div class="grid grid-cols-2 equal-height-cards" style="gap: var(--space-4)">
  <div class="card bg-white">...</div>
  <div class="card bg-white">...</div>
</div>

<!-- Cards with aligned footers -->
<div class="grid grid-cols-2 equal-height-cards aligned-footers" style="gap: var(--space-4)">
  <div class="card bg-white">
    <h2 class="card__title">Card Title</h2>
    <div class="card__content">...</div>
    <div class="card__footer">...</div>
  </div>
  <div class="card bg-white">
    <h2 class="card__title">Card Title</h2>
    <div class="card__content">...</div>
    <div class="card__footer">...</div>
  </div>
</div>
```

### Activity Row

```html
<div class="activity-row">
  <div class="activity-row__content">
    <div class="icon-container icon-small">
      <i class="fas fa-user icon-primary"></i>
    </div>
    <span class="activity-row__text">Activity Text</span>
  </div>
  <div class="activity-row__meta">
    <span class="small-body-text">Meta Text</span>
  </div>
</div>
```

### Tabs

```html
<div class="tabs tabs-large">
  <div class="tab-item active">
    <div class="tab-content">
      <div class="icon-container icon-small">
        <i class="fas fa-globe"></i>
      </div>
      <div class="tab-text">Tab Label</div>
    </div>
    <div class="tab-active-line"></div>
  </div>
  <div class="tab-item">
    <div class="tab-content">
      <div class="icon-container icon-small">
        <i class="fas fa-chart-line"></i>
      </div>
      <div class="tab-text">Another Tab</div>
    </div>
    <div class="tab-active-line"></div>
  </div>
</div>
```

#### Tab Component Requirements

- Always use the `tabs tabs-large` class for the container
- Use `tab-item` for each tab (with `active` class for the active tab)
- Include `tab-content` for the content wrapper
- Use `icon-container icon-small` for icons
- Include `tab-active-line` in all tabs (required for hover effects)
- Don't wrap tabs in cards - they should be standalone components

### Badges

Badges are small, inline components used to display status, counts, or labels. They should be implemented using `<span>` elements.

#### Standard Variants

```html
<!-- Default Badge (Blue) -->
<span class="badge">
  <span class="badge-text">Default</span>
</span>

<!-- Success Badge (Green) -->
<span class="badge badge-success">
  <span class="badge-text">Success</span>
</span>

<!-- Warning Badge (Orange) -->
<span class="badge badge-warning">
  <span class="badge-text">Warning</span>
</span>

<!-- Error Badge (Red) -->
<span class="badge badge-error">
  <span class="badge-text">Error</span>
</span>
```

#### Inline Badge Variant

When a badge needs to be placed inline with text (such as in activity rows or user listings), use the `badge-inline` class to add appropriate spacing:

```html
<!-- Inline Badge (with left margin) -->
<span class="badge badge-success badge-inline">
  <span class="badge-text">Active</span>
</span>
```

Example usage in context:
```html
<div style="display: flex; align-items: center;">
  <div class="icon-container icon-small">
    <i class="fas fa-user-circle icon-muted"></i>
  </div>
  <span class="body-text" style="margin-left: var(--space-2);">John Smith</span>
  <span class="badge badge-success badge-inline">
    <span class="badge-text">Active</span>
  </span>
</div>
```

> ⚠️ **Important**: Always use the `badge-inline` class when placing badges next to text elements, rather than using inline styles for spacing.

#### Using Badges as Labels or Tags

> **Note**: Until dedicated label and tag components are created, the badge component can be used for these purposes. For label-like usage, consider using the default blue badge or the grey badge (`badge-grey`) for a more neutral appearance.

```html
<!-- Label-like usage (grey for neutral appearance) -->
<span class="badge badge-grey">
  <span class="badge-text">Category</span>
</span>

<!-- Tag-like usage -->
<span class="badge">
  <span class="badge-text">Tag Name</span>
</span>
```

#### Custom Color Badges

```html
<!-- Purple Badge -->
<span class="badge badge-purple">
  <span class="badge-text">Purple</span>
</span>

<!-- Grey Badge -->
<span class="badge badge-grey">
  <span class="badge-text">Grey</span>
</span>

<!-- Custom Color Badge (using inline styles) -->
<span class="badge" style="--badge-bg: #6200EA; --badge-text: white;">
  <span class="badge-text">Custom</span>
</span>
```

#### Badges with Icons

```html
<span class="badge badge-success badge-with-icon">
  <div class="icon-container">
    <i class="fas fa-check"></i>
  </div>
  <span class="badge-text">Verified</span>
</span>
```

### Banners

```html
<!-- Default/Info Banner -->
<div class="banner">
  <div class="icon-container icon-small">
    <i class="fas fa-info-circle"></i>
  </div>
  <div class="content">
    <div class="title body-text-medium">Information Message</div>
    <div class="text body-text">This is a standard information banner.</div>
  </div>
  <button class="button-close">
    <div class="icon-container icon-small">
      <i class="fas fa-times"></i>
    </div>
  </button>
</div>

<!-- Warning Banner -->
<div class="banner style-variant-warning">
  <div class="icon-container icon-small">
    <i class="fas fa-exclamation-triangle icon-warning"></i>
  </div>
  <div class="content">
    <div class="title body-text-medium">Warning Alert</div>
    <div class="text body-text">This is a warning banner.</div>
  </div>
  <button class="button-close">
    <div class="icon-container icon-small">
      <i class="fas fa-times"></i>
    </div>
  </button>
</div>
```

#### Key Implementation Details

1. **Structure**: Banners follow a 3-part structure with icon, content, and close button
2. **Typography**: 
   - Always add the `body-text-medium` class to the `.title` element
   - Always add the `body-text` class to the `.text` element
   - The banner CSS only handles layout, not typography
3. **Icons**:
   - Use `icon-container` for consistent icon spacing and alignment
   - Add appropriate semantic color classes for icons (e.g., `icon-warning`)
4. **Close Button**:
   - Wrap the icon in an `icon-container` with `icon-small` class
   - Never apply color classes to close button icons as they have specific hover styles

#### Banner Variants

- **Default/Info**: `.banner` (blue)
- **Warning**: `.banner.style-variant-warning` (orange)
- **Error**: `.banner.style-variant-error` (red)
- **Success**: `.banner.style-variant-success` (green)

For more details on banner placement, see [Banner Placement Guidelines](#banner-placement-guidelines).

### Icons

The icon component provides consistent styling for Font Awesome icons used throughout the system.

```html
<!-- Small Icon (Default - 20x20px) -->
<div class="icon-container icon-small">
  <i class="fas fa-user icon-muted"></i>
</div>

<!-- Medium Icon (24x24px) -->
<div class="icon-container icon-medium">
  <i class="fas fa-user icon-muted"></i>
</div>

<!-- Large Icon (32x32px) -->
<div class="icon-container icon-large">
  <i class="fas fa-user icon-muted"></i>
</div>

<!-- Semantic colors -->
<div class="icon-container icon-small">
  <i class="fas fa-check icon-success"></i>
</div>
<div class="icon-container icon-small">
  <i class="fas fa-exclamation-triangle icon-warning"></i>
</div>
<div class="icon-container icon-small">
  <i class="fas fa-times-circle icon-error"></i>
</div>
<div class="icon-container icon-small">
  <i class="fas fa-info-circle icon-primary"></i>
</div>
```

#### Icon Sizes

The icon component supports three size variations:

| Class | Size | Usage |
|-------|------|-------|
| `icon-small` | 20x20px container with 16x16px icon (default) | Standard UI elements, inline with text |
| `icon-medium` | 24x24px container with 20x20px icon (intermediate size) | Medium emphasis, interactive elements |
| `icon-large` | 32x32px container with 24x24px icon (for emphasis) | High emphasis, featured elements |

#### Icon Colors

| Class | Color | Usage |
|-------|-------|-------|
| `icon-muted` | Grey | Default, neutral actions |
| `icon-primary` | Blue | Primary actions, links |
| `icon-success` | Green | Success states, confirmations |
| `icon-warning` | Orange | Warning states, caution |
| `icon-error` | Red | Error states, destructive actions |

#### Implementation Notes

- Always use the `icon-container` wrapper with an appropriate size class
- Use semantic color classes based on the icon's meaning, not aesthetics
- For Font Awesome icons, always apply the color class to the `<i>` element
- The container handles positioning and layout; the color class handles appearance

## Common Patterns

### Form Card Pattern

```html
<div class="card bg-white">
  <h2 class="card__title">Form Title</h2>
  <div class="card__content" style="display: flex; flex-direction: column; gap: var(--space-4)">
    <div class="form-group">
      <!-- Form inputs -->
    </div>
  </div>
  <div class="card__footer" style="margin-top: var(--space-6)">
    <button class="btn btn-primary btn-medium">
      <span class="btn-text">SUBMIT</span>
    </button>
  </div>
</div>
```

### Activity List Pattern

```html
<div class="card bg-white">
  <h2 class="card__title">Recent Activity</h2>
  <div class="card__content">
    <div class="activity-row">
      <!-- Activity row content -->
    </div>
    <div class="activity-row">
      <!-- Activity row content -->
    </div>
  </div>
</div>
```

## Typography Guidelines

### Typography in Components

When implementing components, always follow these typography rules:

1. **Always Use Typography Classes**: Every text element must use one of the design system's typography classes:
   - `heading-1`, `heading-2`, `heading-3`, `heading-4` for headings
   - `body-text`, `body-text-medium` for standard text
   - `small-body-text`, `small-body-text-medium` for smaller text

2. **Never Define Custom Typography**: Components should never define their own font properties. Instead:
   ```html
   <!-- ✅ CORRECT: Using typography classes -->
   <div class="banner">
     <div class="title body-text-medium">Title Text</div>
     <div class="text body-text">Description text</div>
   </div>
   
   <!-- ❌ INCORRECT: Missing typography classes -->
   <div class="banner">
     <div class="title">Title Text</div>
     <div class="text">Description text</div>
   </div>
   ```

3. **Component CSS Should Extend, Not Replace**: Component CSS should handle layout, spacing, and colors, but typography should come from the design system classes:
   ```css
   /* ✅ CORRECT: CSS focuses on layout, not typography */
   .component .title {
     margin-bottom: var(--space-3);
     color: var(--neutral-grey-800);
   }
   
   /* ❌ INCORRECT: CSS defines typography properties */
   .component .title {
     font-family: var(--body-body-medium-family);
     font-size: var(--body-body-medium-size);
     font-weight: var(--body-body-medium-weight);
     line-height: var(--body-body-medium-line-height);
     margin-bottom: var(--space-3);
   }
   ```

4. **Typography Class Combinations**: When a component needs specific styling beyond typography, combine the typography class with the component class:
   ```html
   <div class="component-title body-text-medium">Title</div>
   ```

Following these guidelines ensures consistent typography across all components and makes the design system more maintainable.

## Banner Placement Guidelines

Banners are important notification elements that should be placed in prominent positions to ensure visibility:

### Page-Level Banners

1. **Primary Placement**: Banners should appear at the top of the page content, immediately:
   - After the header if there are no tabs
   - After the tabs if tabs are present

2. **Example - Banner after header**:
   ```html
   <header class="header">
     <!-- Header content -->
   </header>
   
   <!-- Banner immediately after header -->
   <div class="banner style-variant-success">
     <!-- Banner content -->
   </div>
   
   <section class="section">
     <!-- Page content -->
   </section>
   ```

3. **Example - Banner after tabs**:
   ```html
   <header class="header">
     <!-- Header content -->
   </header>
   
   <div class="tabs tabs-large">
     <!-- Tabs content -->
   </div>
   
   <!-- Banner after tabs -->
   <div class="banner style-variant-success">
     <!-- Banner content -->
   </div>
   
   <section class="section">
     <!-- Page content -->
   </section>
   ```

### Card-Level Banners

1. **Within Cards**: When a banner is specific to a card, place it immediately after the card title:
   ```html
   <div class="card bg-white">
     <h2 class="card__title">Card Title</h2>
     
     <!-- Banner immediately after card title -->
     <div class="banner style-variant-warning">
       <!-- Banner content -->
     </div>
     
     <!-- Add margin-top to create space between banner and content -->
     <div class="card__content" style="margin-top: var(--space-4);">
       <!-- Card content -->
     </div>
   </div>
   ```

2. **Spacing Guidelines**:
   - The banner should not have any margin itself
   - Add `margin-top: var(--space-4)` to the card__content element to create proper spacing
   - This ensures consistent spacing while maintaining the banner's full width within the card

3. **Priority**: Banners should always be the first element after the title to ensure they're noticed before the user engages with the content.

Following these placement guidelines ensures that important notifications are visible and properly positioned in the interface hierarchy. 

## Best Practices and Common Mistakes

### General Component Mistakes

1. **Missing required wrapper elements**
   - Many components require specific wrapper elements with specific class names
   - Always check the component documentation for the required structure

2. **Incorrect class combinations**
   - Components often require multiple classes used together
   - Base classes + variant classes + size classes are typically all required

3. **Inconsistent nesting**
   - Maintain consistent nesting patterns across similar components
   - Follow the examples in the documentation exactly

### Specific Component Issues

1. **Buttons**
   - Always include a style variant (`btn-primary` or `btn-secondary`)
   - Always include a size class (`btn-medium` or `btn-small`)
   - Always wrap text in `<span class="btn-text">`
   - Always wrap icons in `<div class="btn-icon">`
   - Use `text-white` for icons in primary buttons
   - Use `icon-muted` for icons in secondary buttons

2. **Form Elements**
   - Maintain the full wrapper structure for all form elements
   - Don't skip intermediate wrapper elements even if they seem unnecessary
   - Wrap each form element in a `.form-group` div
   - Use grid or flex with gap for complex form layouts

3. **Layout Components**
   - Follow the exact class naming conventions for different sections
   - Use the correct background classes (e.g., `bg-white`) as needed
   - Use `bg-grey-50` on body element
   - Wrap content in `container page-container` with padding: var(--space-16)
   - Use `content-wrapper` with gap for spacing between sections

### Typography Best Practices

- ✅ Use typography classes instead of direct font properties
- ✅ Follow the font-weight guidelines
- ✅ Include proper text color classes
- ❌ Don't mix typography classes incorrectly
- ❌ Don't skip small-body-text for subtitles
- ❌ Don't use raw font-size or font-weight values

### Layout Best Practices

- ✅ Use gap-based spacing instead of margins between components
- ❌ Don't skip page-container class
- ❌ Don't forget padding: var(--space-16) on page-container
- ❌ Don't use raw pixel values for gaps
- ❌ Don't add margins to sections when using gap-based spacing
- ❌ Don't wrap tabs in card components

### Spacing Best Practices

- ✅ Use the content-wrapper's gap property (var(--space-6)) for spacing between sections
- ✅ Use consistent 16px gap (var(--space-4)) for all card layouts
- ✅ Maintain component-specific internal spacing (like card footer margin-top)
- ✅ Use 12px gap (var(--space-3)) between icons and text
- ❌ Don't add margins to sections when using gap-based spacing
- ❌ Don't mix margin-based and gap-based spacing at the same level
- ❌ Don't use raw pixel values instead of spacing variables
- ❌ Don't use different gap values for cards within the same layout 

## Responsive Grid Layouts

The design system provides responsive grid classes that automatically adjust their layout based on screen size.

### Responsive Grid Classes

Instead of using fixed column counts or inline styles, use these responsive grid classes:

```html
<!-- For KPI/Overview cards (4-2-1 columns) -->
<div class="grid-responsive-kpi">
  <!-- Cards -->
</div>

<!-- For content cards (2-1 columns) -->
<div class="grid-responsive-cards">
  <!-- Cards -->
</div>

<!-- For small cards (4-1 columns) -->
<div class="grid-responsive-small">
  <!-- Cards -->
</div>
```

### Breakpoints

These classes use the following breakpoints:

| Class | Large (>1024px) | Medium (768-1024px) | Small (576-768px) | Extra Small (<576px) |
|-------|----------------|---------------------|-------------------|----------------------|
| `grid-responsive-kpi` | 4 columns | 2 columns | 2 columns | 1 column |
| `grid-responsive-cards` | 2 columns | 2 columns | 1 column | 1 column |
| `grid-responsive-small` | 4 columns | 4 columns | 1 column | 1 column |

This creates balanced layouts at different screen sizes:
- At large screens, KPI cards show in a row of 4
- At medium screens, KPI cards show in a 2×2 grid
- At small screens, cards stack in a single column

### Balanced Layouts for Uneven Numbers

For more balanced layouts with specific numbers of cards, add these modifier classes:

```html
<!-- For 3 KPI cards (single row of 3) -->
<div class="grid-responsive-kpi grid-3-cards">
  <!-- 3 cards -->
</div>

<!-- For 5 KPI cards (3-2 layout) -->
<div class="grid-responsive-kpi grid-5-cards">
  <!-- 5 cards -->
</div>
```

#### For 5 KPI Cards with `grid-5-cards` class:
- Large screens: 3-2 layout (3 cards in first row, 2 in second)
- Medium screens: 3-2 layout
- Small screens: Single column

#### For 3 KPI Cards with `grid-3-cards` class:
- Large screens: Single row of 3
- Medium screens: Single row of 3
- Small screens: Single column

This ensures that cards are distributed evenly across rows, with more cards in the first row if the number is not even.

### Example Implementation

```html
<!-- 5 KPI cards with balanced 3-2 layout -->
<section class="section">
  <div class="grid-responsive-kpi grid-5-cards">
    <div class="overview-card bg-white"><!-- Card 1 --></div>
    <div class="overview-card bg-white"><!-- Card 2 --></div>
    <div class="overview-card bg-white"><!-- Card 3 --></div>
    <div class="overview-card bg-white"><!-- Card 4 --></div>
    <div class="overview-card bg-white"><!-- Card 5 --></div>
  </div>
</section>
```

### Fixed vs Responsive Grid

While the design system still supports fixed column grids, responsive grids are recommended for most use cases:

```html
<!-- Fixed 4-column grid (not recommended) -->
<div class="grid grid-cols-4" style="gap: var(--space-4)">
  <!-- Grid items -->
</div>

<!-- Responsive grid (recommended) -->
<div class="grid-responsive-kpi">
  <!-- Grid items -->
</div>
```

This approach ensures your layouts adapt gracefully to different screen sizes with predictable breakpoints.

## Navigation Component

The topbar component creates a consistent application navigation bar with project selection, context switching, tools, and user profiles.

#### Required Structure

```
topbar
└── topbar__header
    └── topbar__container
        ├── topbar__section-primary
        │   ├── topbar__branding
        │   │   ├── topbar__logo
        │   │   ├── topbar__details
        │   │   │   ├── topbar__subtitle
        │   │   │   └── topbar__title
        │   │   └── icon-container
        │   └── topbar__context
        │       ├── topbar__context-name
        │       └── icon-container
        └── topbar__section-secondary
            ├── [search component]
            ├── topbar__actions
            │   └── icon-container.topbar__action-item
            └── topbar__avatar
                └── img
```

#### HTML Implementation

```html
<!-- Topbar Component -->
<nav class="topbar">
    <!-- Header section with logo, project info, and user controls -->
    <div class="topbar__header">
        <div class="topbar__container">
            <!-- Left section with project and context -->
            <div class="topbar__section-primary">
                <!-- Branding with correct logo -->
                <div class="topbar__branding">
                    <img 
                        src="../assets/logos/logo_navigation.svg" 
                        alt="Keboola Logo" 
                        class="topbar__logo"
                        width="24" 
                        height="42"
                    >
                    <div class="topbar__details">
                        <p class="topbar__subtitle small-body-text">Organization Name</p>
                        <p class="topbar__title body-text-medium">Project Name</p>
                    </div>
                    <div class="icon-container icon-small">
                        <i class="fas fa-chevron-down icon-muted"></i>
                    </div>
                </div>
                
                <!-- Context selector -->
                <div class="topbar__context">
                    <span class="topbar__context-name body-text">Environment</span>
                    <div class="icon-container icon-small">
                        <i class="fas fa-chevron-down icon-muted"></i>
                    </div>
                </div>
            </div>
            
            <!-- Right section -->
            <div class="topbar__section-secondary">
                <!-- Search -->
                <div class="text-input size-medium">
                    <div class="content" style="min-height: 40px;">
                        <i class="fas fa-search" style="color: var(--neutral-grey-400);"></i>
                        <input type="text" placeholder="Search" aria-label="Search">
                    </div>
                </div>
                
                <!-- Action Icons -->
                <div class="topbar__actions">
                    <div class="icon-container icon-large topbar__action-item">
                        <i class="fas fa-bell icon-muted"></i>
                        <div class="topbar__indicator">3</div>
                    </div>
                </div>
                
                <!-- Avatar with correct placeholder -->
                <div class="topbar__avatar">
                    <img src="../assets/avatars/placeholder.png" alt="User Avatar">
                </div>
            </div>
        </div>
    </div>
</nav>
```

#### CSS Variables

The topbar component uses these key CSS variables for consistent styling:

```css
--topbar-height: 68px;       /* Controls the height of the topbar */
--content-top-spacing: 32px; /* Controls spacing from top of content area */
```

#### Interactive Elements

The topbar includes interactive elements with hover effects:

1. **Action Icons**: When hovering over an action icon in the topbar, the icon changes color from gray to blue
   ```css
   /* The container has the action item class */
   .topbar__action-item.icon-container:hover {
       color: var(--secondary-blue-500-base);
   }
   
   /* Make sure nested icons also change color on hover */
   .topbar__action-item.icon-container:hover i {
       color: var(--secondary-blue-500-base);
   }
   ```

2. **Avatar**: The user avatar has a subtle background color change on hover
   ```css
   .topbar__avatar:hover {
       background-color: var(--neutral-grey-200);
   }
   ```

#### Responsive Behavior

The topbar component adapts to different screen sizes:

```css
@media (max-width: 768px) {
    :root {
        --topbar-height: 60px; /* Smaller height on mobile */
    }
    
    .topbar__section-primary {
        gap: var(--space-2);
    }
    
    .topbar__container {
        padding: 0 var(--space-4);
    }
}
```

#### Important Implementation Notes

1. **Page Container Spacing**: When using the topbar component, add this class to your page container:
   ```html
   <div class="container page-container">
   ```
   The `page-container` class automatically adds margin-top to clear the fixed topbar.

2. **Pages Without Topbar**: Use the `no-topbar` class on the body for pages without a topbar:
   ```html
   <body class="no-topbar">
   ```

3. **Preventing Layout Shift**: Add this to your critical CSS to prevent layout shifts on load:
   ```html
   <style>
       .topbar {
           height: 68px;
           position: fixed;
           top: 0;
           left: 0;
           right: 0;
           background-color: white;
           z-index: 100;
           border-bottom: 1px solid #EAEAEA;
       }
       .page-container {
           margin-top: 68px;
       }
   </style>
   ```

4. **Action Icons**: Use the `topbar__action-icon` class for all icons in the topbar, regardless of their specific purpose, to ensure consistent styling:
   ```html
   <i class="fas fa-[icon-name] icon-muted topbar__action-icon"></i>
   ```

5. **Notification Indicators**: Add notification badges with the `topbar__indicator` class:
   ```html
   <div class="topbar__indicator">5</div>
   ```

## Icon Component

The icon component provides a standardized way to display Font Awesome icons with consistent sizing and styling throughout the application.

### Icon Sizes

- **icon-small**: 20x20px container with 16x16px icon (default)
- **icon-medium**: 24x24px container with 20x20px icon (intermediate size)
- **icon-large**: 32x32px container with 24x24px icon (for emphasis)

### Implementation

```html
<!-- Small Icon (Default - 20x20px) -->
<div class="icon-container icon-small">
  <i class="fas fa-user icon-muted"></i>
</div>

<!-- Medium Icon (24x24px) -->
<div class="icon-container icon-medium">
  <i class="fas fa-user icon-muted"></i>
</div>

<!-- Large Icon (32x32px) -->
<div class="icon-container icon-large">
  <i class="fas fa-user icon-muted"></i>
</div>
```

### Best Practices

1. Always wrap icons in `icon-container` for consistent spacing and alignment
2. Always specify the size class (`icon-small`, `icon-medium`, or `icon-large`)
3. Use semantic color classes only when the icon represents a status:
   - `icon-success`: Green for success states
   - `icon-warning`: Orange for warning states
   - `icon-error`: Red for error states
   - `icon-muted`: Default grey for most UI icons (recommended default)
4. For interactive icons, add appropriate hover effects by wrapping in a button or applying hover styles

### Topbar Component

The topbar provides consistent navigation and context across all Keboola applications.

#### Logo Implementation

The topbar uses a specific navigation-optimized logo variant:

```html
<div class="topbar__branding">
    <img 
        src="../assets/logos/logo_navigation.svg" 
        alt="Keboola Logo" 
        class="topbar__logo"
        width="24" 
        height="42"
    >
    <!-- ... rest of branding content ... -->
</div>
```

**Important Logo Guidelines:**
- Always use `logo_navigation.svg` for the topbar (NOT `logo.svg`)
- Maintain dimensions: width="24" height="42"
- The navigation logo is taller than wide (1:1.75 ratio)
- General `logo.svg` is square (1:1) and should NOT be used in the topbar

#### Avatar Implementation

The user avatar in the topbar follows these specifications:

```html
<div class="topbar__avatar">
    <img 
        src="../assets/avatars/placeholder.png" 
        alt="User Avatar"
    >
</div>
```

**Important Avatar Guidelines:**
- Default placeholder: `placeholder.png` in assets/avatars/
- The avatar container handles the circular shape via CSS
- No need to specify dimensions - handled by topbar__avatar class
- Ensure avatar images are square for proper circular cropping

#### Full Topbar Structure

```html
<nav class="topbar">
    <div class="topbar__header">
        <div class="topbar__container">
            <!-- Left section -->
            <div class="topbar__section-primary">
                <!-- Branding with correct logo -->
                <div class="topbar__branding">
                    <img src="../assets/logos/logo_navigation.svg" alt="Keboola Logo" class="topbar__logo" width="24" height="42">
                    <div class="topbar__details">
                        <p class="topbar__subtitle small-body-text">Organization Name</p>
                        <p class="topbar__title body-text-medium">Project Name</p>
                    </div>
                    <div class="icon-container icon-small">
                        <i class="fas fa-chevron-down icon-muted"></i>
                    </div>
                </div>
                
                <!-- Context selector -->
                <div class="topbar__context">
                    <span class="topbar__context-name body-text">Environment</span>
                    <div class="icon-container icon-small">
                        <i class="fas fa-chevron-down icon-muted"></i>
                    </div>
                </div>
            </div>
            
            <!-- Right section -->
            <div class="topbar__section-secondary">
                <!-- Search -->
                <div class="text-input size-medium">
                    <div class="content" style="min-height: 40px;">
                        <i class="fas fa-search" style="color: var(--neutral-grey-400);"></i>
                        <input type="text" placeholder="Search" aria-label="Search">
                    </div>
                </div>
                
                <!-- Action Icons -->
                <div class="topbar__actions">
                    <div class="icon-container icon-large topbar__action-item">
                        <i class="fas fa-bell icon-muted"></i>
                        <div class="topbar__indicator">3</div>
                    </div>
                </div>
                
                <!-- Avatar with correct placeholder -->
                <div class="topbar__avatar">
                    <img src="../assets/avatars/placeholder.png" alt="User Avatar">
                </div>
            </div>
        </div>
    </div>
</nav>
```

#### Typography Classes

- Organization name: `small-body-text`
- Project name: `body-text-medium`
- Context name: `body-text`

#### Asset Requirements

Required assets must be available at:
- `assets/logos/logo_navigation.svg` - Navigation-specific logo
- `assets/avatars/placeholder.png` - Default avatar placeholder

## Asset Requirements

### Required Assets Structure

```assets/
├── logos/
│   ├── logo.svg           # Square logo (1:1) for general use
│   └── logo_navigation.svg # Tall logo (1:1.75) for navigation
└── avatars/
    └── placeholder.png    # Default avatar placeholder
```

### Logo Usage Guidelines

- `logo.svg`: General purpose, square ratio (1:1)
  - Use for: marketing, documentation, general branding
  - Dimensions: Flexible, maintains square ratio

- `logo_navigation.svg`: Navigation-specific, tall ratio (1:1.75)
  - Use for: Topbar navigation only
  - Fixed dimensions: 24x42px
  - Do not use for general purposes

### Avatar Guidelines

- Default placeholder: `placeholder.png`
- Used in: Topbar, user profiles
- Container handles circular cropping
- Always provide square images for consistent circular display

## Support & Contributing

### Support & Documentation

If you need help implementing any component from the Keboola Design System:

1. Check the detailed documentation in both README.md and COMPONENT-GUIDE.md
2. Review the example implementations in the /examples directory
3. For further assistance, please contact the design system team

### Contributing

When contributing to the Keboola Design System:

1. Follow the established patterns and conventions
2. Test components across different browsers and screen sizes
3. Ensure accessibility compliance with WCAG 2.1 standards
4. Document any new components or modifications
5. Update example pages as needed