# Page Workflow

Complete workflow for building pages using the design system.
Read this when the mode is **Pagina**.

---

## Step 1: Analyze the Design

Look at the screenshot or Figma design and identify:

### Layout Structure
- How many main sections/columns?
- Is there a sidebar? Header? Footer?
- Grid structure (1-column, 2-column, 3-column)
- Container widths and spacing patterns

### UI Sections
Break the page into logical sections (top to bottom, left to right).
Name each by its purpose:
- "Sidebar Navigation"
- "Dashboard Header"
- "Metrics Cards Row"
- "Data Table Section"
- "Chat Panel"

### Content Hierarchy
- Primary headings
- Main content vs. supporting content
- Call-to-action elements
- Data visualization elements

---

## Step 2: Map to Existing Components (CRITICAL)

**Rule: IMPORT before CREATE.**

### 2a. Check what exists in the project

```
1. List components/ui/ -- all shadcn base components
2. List components/ -- all custom components
3. Read showcase pages in styleguide/ -- understand available variants
```

### 2b. Map each visual element

Create a mapping table:

| Visual Element | Existing Component | Action |
|----------------|-------------------|--------|
| Navigation sidebar | Sidebar (shadcn) | Import |
| Metric cards | InsightCard (custom) | Import |
| Data table | Table (shadcn) | Import |
| Status badges | BadgeStatus (custom) | Import |
| Action buttons | Button (shadcn) | Import |
| Search input | Input (shadcn) | Import |
| Chart | Chart (shadcn) | INSTALL -- not yet in project |
| Custom widget | -- | BUILD -- nothing similar exists |

### 2c. Categorize actions

- **Import:** component already exists in the project
- **Install:** exists in shadcn but not yet installed
- **Build:** doesn't exist anywhere, needs to be created
- **Extend:** exists but needs a new variant

**If BUILD is needed:** follow the Component Workflow first, THEN return
to the page build.

---

## Step 3: Install Missing Components

```bash
npx shadcn@latest add [component1] [component2] [component3]
```

Only install what's actually needed for this page.

---

## Step 4: Build the Page

Create `/app/[page-name]/page.tsx`:

### Structure pattern

```tsx
import { Card, CardHeader, CardContent } from "@/components/ui/card"
import { Button } from "@/components/ui/button"
import { Badge } from "@/components/ui/badge"
// Import from EXISTING design system components
import { InsightCard } from "@/components/ui/insight-card"

export default function PageName() {
  return (
    <div className="flex min-h-screen">
      {/* Sidebar (if present) */}
      <aside className="w-64 border-r bg-sidebar">
        {/* Sidebar content */}
      </aside>

      {/* Main content */}
      <main className="flex-1">
        {/* Header */}
        <header className="border-b p-4">
          {/* Header content */}
        </header>

        {/* Page content */}
        <div className="p-6 space-y-6">
          {/* Sections */}
        </div>
      </main>
    </div>
  )
}
```

### Styling rules

**Colors (always CSS variables via Tailwind):**
- Backgrounds: `bg-background`, `bg-card`, `bg-muted`, `bg-sidebar`
- Text: `text-foreground`, `text-muted-foreground`, `text-primary`
- Borders: `border-border`
- Accents: `bg-primary`, `text-primary-foreground`

**Spacing (8pt grid via Tailwind):**
- `p-2` (8px), `p-3` (12px), `p-4` (16px), `p-6` (24px), `p-8` (32px)
- `gap-2`, `gap-4`, `gap-6`, `gap-8`
- `space-y-4`, `space-y-6`, `space-y-8`

**Never use:**
- Hardcoded hex colors (`text-[#f97316]`)
- Arbitrary spacing (`p-[13px]`)
- Inline styles for colors or spacing

---

## Step 5: Responsive Behavior

Design mobile-first, then enhance for larger screens.

### Breakpoints

| Breakpoint | Width | Layout |
|-----------|-------|--------|
| Mobile | < 768px | Single column, sidebar hidden, full-width elements |
| Tablet | 768-1024px | Sidebar as overlay or mini, 2 columns where appropriate |
| Desktop | > 1024px | Full layout as designed |

### Common responsive patterns

```tsx
{/* Sidebar: hidden on mobile, visible on desktop */}
<aside className="hidden md:block md:w-64">

{/* Grid: 1 col mobile, 2 cols tablet, 3 cols desktop */}
<div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4">

{/* Stack on mobile, row on desktop */}
<div className="flex flex-col md:flex-row gap-4">

{/* Full width button on mobile, auto on desktop */}
<Button className="w-full md:w-auto">
```

### Mobile considerations
- Touch targets: minimum 44x44px
- No hover-only interactions
- Bottom navigation if sidebar collapses
- Full-width cards and inputs
- Simplified data displays (hide non-essential columns)

---

## Step 6: Post-Build Verification

After building the page, run these checks:

### Design System Compliance

- [ ] All colors reference CSS variables (no hardcoded hex)
- [ ] All spacing values from 8pt grid
- [ ] All components imported from DS (no inline recreations)
- [ ] Border-radius consistent with DS settings
- [ ] Typography uses DS scale

### Functional

- [ ] Page renders without errors
- [ ] Responsive at 375px, 768px, 1200px+
- [ ] Interactive elements work (buttons, tabs, forms)
- [ ] Loading and error states considered
- [ ] Empty states handled

### Accessibility

- [ ] Color contrast 4.5:1 for text
- [ ] Touch targets 44x44px minimum
- [ ] Semantic HTML (headings, nav, main, aside)
- [ ] Keyboard navigable
- [ ] Images have alt text

**If any check fails:** fix before reporting completion.

---

## Step 7: Report

After building, provide:

```
Page: [name]
Location: /app/[page-name]/page.tsx

Sections built:
1. [Section name] -- [components used]
2. [Section name] -- [components used]

Components used:
- Imported from DS: [list]
- Newly installed: [list]
- Custom built: [list] (showcase pages created: yes/no)

Responsive: [confirmed at 375px, 768px, 1200px+]

Notes: [anything the user should know]
```

---

## Notes

- **Works with any visual input:** screenshots, Figma designs, rough mockups
- **Visual analysis first** -- understand the design before mapping to components
- **shadcn MCP** for verifying components and getting install commands
- **CSS variables** for ALL colors
- **Mobile-first** responsive approach
- **Import from DS** -- never recreate what already exists
- If the AI creates a component that already exists in the DS, refactor immediately
