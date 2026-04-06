# Foundation Workflow

Complete workflow for creating or extracting a design system foundation.
Read this when the mode is **Foundation**.

---

## Entry Point A: From Screenshot (New Project)

### 1. Analyze the Design

Look at the screenshot and extract:

**Colors:**
- Primary/brand color -- generate full scale (50-900)
- Neutral/grey colors -- generate full scale (50-900)
- Semantic colors (success, error, warning, info)
- Background and surface colors
- Border colors

**Typography:**
- Font family (identify from the design or infer)
- Heading sizes and weights
- Body text sizes

**Spacing & Radius:**
- Spacing rhythm (tight, normal, relaxed)
- Border radius style (sharp 0-4px, rounded 8-12px, pill 16px+)

**Shadows:**
- Shadow style (none, subtle, prominent)

### 2. Initialize shadcn

```bash
npx shadcn@latest init
```

When prompted:
- Style: Default
- Base color: Neutral (will be overridden)
- CSS variables: Yes

### 3. Generate globals.css

Replace `/app/globals.css` with extracted tokens.

**Required structure:**

```css
@import "tailwindcss";

:root {
  /* === BASE === */
  --background: [page background];
  --foreground: [text color];

  /* === SURFACES === */
  --card: [card background];
  --card-foreground: [card text];
  --popover: [popover background];
  --popover-foreground: [popover text];

  /* === BRAND === */
  --primary: [main brand color];
  --primary-foreground: [contrast text];
  --secondary: [muted version];
  --secondary-foreground: [text];

  /* === FEEDBACK === */
  --muted: [light grey background];
  --muted-foreground: [medium grey text];
  --accent: [subtle tint];
  --accent-foreground: [text];
  --destructive: [red/error];
  --destructive-foreground: [white];
  --success: [green];
  --success-foreground: [white];
  --warning: [yellow/orange];
  --warning-foreground: [dark for contrast];
  --info: [blue];
  --info-foreground: [white];

  /* === UTILITY === */
  --border: [border color];
  --input: [input border];
  --ring: [focus ring color];
  --radius: [default border radius];

  /* === CHARTS === */
  --chart-1: [primary];
  --chart-2: [complementary];
  --chart-3 through --chart-5: [variations];

  /* === SIDEBAR === */
  --sidebar: [sidebar bg];
  --sidebar-foreground: [sidebar text];
  --sidebar-primary: [primary];
  --sidebar-primary-foreground: [contrast];
  --sidebar-accent: [accent];
  --sidebar-accent-foreground: [text];
  --sidebar-border: [border];
  --sidebar-ring: [ring];
}

.dark {
  /* ALL variables redefined for dark mode */
  /* Use darker backgrounds, lighter text */
  /* Desaturate primary colors slightly */
  /* Shadows become lighter surface colors */
}

@theme inline {
  --color-background: var(--background);
  --color-foreground: var(--foreground);
  --color-card: var(--card);
  --color-card-foreground: var(--card-foreground);
  --color-popover: var(--popover);
  --color-popover-foreground: var(--popover-foreground);
  --color-primary: var(--primary);
  --color-primary-foreground: var(--primary-foreground);
  --color-secondary: var(--secondary);
  --color-secondary-foreground: var(--secondary-foreground);
  --color-muted: var(--muted);
  --color-muted-foreground: var(--muted-foreground);
  --color-accent: var(--accent);
  --color-accent-foreground: var(--accent-foreground);
  --color-destructive: var(--destructive);
  --color-destructive-foreground: var(--destructive-foreground);
  --color-border: var(--border);
  --color-input: var(--input);
  --color-ring: var(--ring);
  --color-sidebar: var(--sidebar);
  --color-sidebar-foreground: var(--sidebar-foreground);
  --color-success: var(--success);
  --color-success-foreground: var(--success-foreground);
  --color-warning: var(--warning);
  --color-warning-foreground: var(--warning-foreground);
  --color-info: var(--info);
  --color-info-foreground: var(--info-foreground);
}

body {
  background: var(--background);
  color: var(--foreground);
}
```

**Color generation rules:**
- Generate harmonious scales using color theory (50-900)
- Ensure 4.5:1 contrast ratio for text (WCAG AA)
- Chart colors must be visually distinct from each other
- When colors aren't clearly visible in reference, make reasonable inferences
- Use shadcn defaults as fallback when uncertain

### 4. Install Font

Add to `/app/layout.tsx`:

```tsx
import { Inter } from 'next/font/google' // or matched font

const font = Inter({ subsets: ['latin'] })

export default function RootLayout({ children }) {
  return (
    <html lang="en">
      <body className={font.className}>{children}</body>
    </html>
  )
}
```

### 5. Install Base Components

```bash
npx shadcn@latest add button card badge alert radio-group
```

### 6. Create Styleguide Structure

**navigation.ts** -- navigation config:

```ts
export interface NavItem {
  name: string
  href: string
}

export interface NavSection {
  title: string
  items: NavItem[]
}

export const navigation: NavSection[] = [
  {
    title: "Foundation",
    items: [
      { name: "Design Tokens", href: "/styleguide" },
    ]
  },
  {
    title: "Components",
    items: []
  }
]
```

**layout.tsx** -- styleguide layout with sidebar navigation.

**page.tsx** -- displays ALL design tokens:
- Color palette (all colors as swatches with variable names)
- Primary scale (50-900)
- Grey/neutral scale (50-900)
- Semantic colors (success, warning, error, info)
- Typography (heading and body samples)
- Border radius (examples of each size)
- Shadows (shadow examples)
- Base components (button, card, badge, alert, radio-group)
- Dark mode toggle (preview both themes)

### 7. Output Design Summary

```
Design Summary:
- Primary color: [hex] ([color name])
- Font: [font name]
- Style: [e.g., "Modern minimal", "Bold colorful", "Soft friendly"]
- Border radius: [e.g., "Rounded 8px", "Sharp", "Pill"]
- Overall feel: [brief description]
```

---

## Entry Point B: From Existing Project (Extract & Organize)

### 1. Scan for Existing Values

Search the project for all design values currently in use:

```
Colors:     grep for hex (#), rgb(), hsl(), oklch() in CSS/TSX files
Spacing:    grep for p-[X], m-[X], gap-[X], padding:, margin:
Typography: grep for text-[X], font-[X], font-size:, font-weight:
Radius:     grep for rounded-[X], border-radius:
Shadows:    grep for shadow-[X], box-shadow:
```

### 2. Categorize Findings

Group discovered values into:
- **Already tokenized:** values referencing CSS variables (good)
- **Hardcoded but consistent:** same value used multiple times (should be tokenized)
- **Hardcoded and inconsistent:** variations of similar values (need consolidation)
- **One-offs:** used only once (evaluate if needed)

### 3. Create Token Inventory

Present findings to user:

```
Token Inventory - [Project Name]

Already Tokenized: [X] values
| Category | Count | Examples |
|----------|-------|----------|
| Colors   | X     | --primary, --background |
| Spacing  | X     | --space-4, --space-6 |

Needs Tokenization: [X] values
| Value | Used In | Occurrences | Suggested Token |
|-------|---------|-------------|-----------------|
| #f97316 | Header, CTA | 8 | --primary |
| 12px | cards, modals | 15 | --radius |

Inconsistencies Found: [X]
| Pattern | Variations | Suggestion |
|---------|-----------|------------|
| Grey text | #666, #6b7280, #71717a | Consolidate to --muted-foreground |
```

### 4. Propose Token Structure

Based on findings, propose a `globals.css` structure. Get user approval
before applying changes.

### 5. Migrate Hardcoded Values

After approval:
1. Create/update `globals.css` with organized tokens
2. Replace hardcoded values with Tailwind classes referencing tokens
3. Create styleguide if it doesn't exist
4. Report what was migrated and what remains

---

## Notes

- If colors aren't clearly visible in a screenshot, make reasonable inferences
- Generate harmonious color scales using color theory
- Ensure sufficient contrast for accessibility (4.5:1 for text)
- Chart colors should be visually distinct
- When in doubt, use shadcn defaults as fallback
- For existing projects: NEVER change visual appearance -- only organize values into tokens
