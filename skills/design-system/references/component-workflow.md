# Component Workflow

Complete workflow for adding components to the design system.
Read this when the mode is **Componente**.

---

## Pre-flight: Check for Duplicates (MANDATORY)

Before installing or building anything:

1. **Search the project** for existing implementations:
   ```
   Glob: components/**/*[component-name]*
   Grep: "ComponentName" in components/, app/
   ```

2. **If found:** Report to user. Suggest using the existing component or
   refactoring it into the design system instead of creating a new one.

3. **If similar but different:** Report both implementations. Ask user
   which pattern should be the canonical one.

Only proceed to installation after confirming no duplicates exist.

---

## Step 1: Search shadcn Registry

Use shadcn MCP (if available) or manual search:

- **Search:** `search_items_in_registries` with query "[component name]"
- **View details:** `view_items_in_registries` to see structure and dependencies
- **Get examples:** `get_item_examples_from_registries` with query "[component]-demo"

**Decision tree:**
- Component exists in shadcn → Step 2 (Install)
- Component doesn't exist → Step 4 (Build Custom)

### Common shadcn components reference

| Category | Components |
|----------|-----------|
| **Layout** | Card, Separator, Tabs, Accordion, Collapsible, Resizable |
| **Forms** | Button, Input, Select, Checkbox, Radio, Switch, Textarea, Label, Form, Slider, Toggle |
| **Feedback** | Alert, Toast/Sonner, Progress, Skeleton, Badge |
| **Overlay** | Dialog, Drawer, Popover, Tooltip, Dropdown Menu, Context Menu, Alert Dialog, Sheet, Hover Card |
| **Navigation** | Navigation Menu, Breadcrumb, Pagination, Command, Menubar, Sidebar |
| **Data** | Table, Data Table, Calendar, Chart, Carousel, Scroll Area |

---

## Step 2: Install shadcn Component

```bash
npx shadcn@latest add [component-name]
```

After installation:
1. Read the installed file in `components/ui/`
2. Understand available variants, props, and how it uses CSS variables
3. Verify it renders correctly with current tokens

---

## Step 3: Customize Component (if needed)

If the base component needs additional variants or behavior, create a wrapper.

**Rules:**
- Wrapper goes in `/components/[ComponentName].tsx` (NOT in `components/ui/`)
- Always extend the shadcn component, never copy-paste and modify
- Use `cn()` for class merging
- All colors via CSS variables (Tailwind classes like `bg-success`, never hex)
- Export both the wrapper and re-export the base for flexibility

**Pattern:**

```tsx
import { Button } from "@/components/ui/button"
import { cn } from "@/lib/utils"

interface CustomButtonProps extends React.ComponentProps<typeof Button> {
  intent?: 'default' | 'success' | 'warning' | 'info'
  loading?: boolean
}

export function CustomButton({
  intent = 'default',
  loading = false,
  className,
  children,
  disabled,
  ...props
}: CustomButtonProps) {
  return (
    <Button
      className={cn(
        intent === 'success' && 'bg-success text-success-foreground hover:bg-success/90',
        intent === 'warning' && 'bg-warning text-warning-foreground hover:bg-warning/90',
        intent === 'info' && 'bg-info text-info-foreground hover:bg-info/90',
        className
      )}
      disabled={disabled || loading}
      {...props}
    >
      {loading ? (
        <span className="flex items-center gap-2">
          <span className="h-4 w-4 animate-spin rounded-full border-2 border-current border-t-transparent" />
          {children}
        </span>
      ) : children}
    </Button>
  )
}
```

---

## Step 4: Build Custom Component (not in shadcn)

If shadcn doesn't have the component:

1. **Use shadcn primitives** as building blocks (cn, cva if needed)
2. **Follow shadcn patterns:** same prop interface style, className support, forwardRef
3. **CSS variables only** via Tailwind classes
4. **Place in** `/components/[ComponentName].tsx`

**Pattern:**

```tsx
import { cn } from "@/lib/utils"

interface StatusCardProps {
  variant?: 'default' | 'success' | 'warning' | 'error'
  title: string
  value: string
  description?: string
  className?: string
}

export function StatusCard({
  variant = 'default',
  title,
  value,
  description,
  className
}: StatusCardProps) {
  return (
    <div className={cn(
      "rounded-lg border p-4 space-y-2",
      variant === 'default' && 'bg-card text-card-foreground border-border',
      variant === 'success' && 'bg-success/10 text-success border-success/20',
      variant === 'warning' && 'bg-warning/10 text-warning border-warning/20',
      variant === 'error' && 'bg-destructive/10 text-destructive border-destructive/20',
      className
    )}>
      <p className="text-sm text-muted-foreground">{title}</p>
      <p className="text-2xl font-bold">{value}</p>
      {description && (
        <p className="text-sm text-muted-foreground">{description}</p>
      )}
    </div>
  )
}
```

---

## Step 5: Create Showcase Page

Create `/app/styleguide/components/[component-name]/page.tsx` with:

### Required sections

1. **Title and description** -- what the component is and when to use it
2. **All variants** -- every visual variation side by side
3. **All sizes** -- if the component has size variants
4. **All states** -- default, hover, focus, disabled, loading, error
5. **Dark mode preview** -- toggle to see dark mode rendering
6. **Composition examples** -- component used with other components
7. **Code examples** -- import statement and basic usage

### Showcase structure

```tsx
export default function ComponentShowcase() {
  return (
    <div className="p-8 space-y-12">
      <div>
        <h1 className="text-3xl font-bold mb-2">Component Name</h1>
        <p className="text-muted-foreground">Brief description and when to use.</p>
      </div>

      {/* Variants */}
      <section className="space-y-4">
        <h2 className="text-xl font-semibold">Variants</h2>
        <div className="flex flex-wrap gap-4">
          {/* Each variant */}
        </div>
      </section>

      {/* Sizes */}
      <section className="space-y-4">
        <h2 className="text-xl font-semibold">Sizes</h2>
        <div className="flex items-end gap-4">
          {/* Each size */}
        </div>
      </section>

      {/* States */}
      <section className="space-y-4">
        <h2 className="text-xl font-semibold">States</h2>
        <div className="flex flex-wrap gap-4">
          {/* default, disabled, loading, etc. */}
        </div>
      </section>

      {/* Usage */}
      <section className="space-y-4">
        <h2 className="text-xl font-semibold">Usage</h2>
        <pre className="bg-muted p-4 rounded-lg text-sm overflow-x-auto">
          {`import { ComponentName } from "@/components/ui/component-name"

<ComponentName variant="default" />`}
        </pre>
      </section>
    </div>
  )
}
```

---

## Step 6: Update Navigation

Add to `/app/styleguide/navigation.ts`:

```ts
{
  title: "Components",
  items: [
    // ... existing components
    { name: "[Component Name]", href: "/styleguide/components/[component-name]" },
  ]
}
```

**Keep alphabetical order** within the Components section.

---

## Step 7: Verification Checklist

Before reporting completion:

- [ ] Component uses CSS variables (no hardcoded colors)
- [ ] All variants work correctly
- [ ] Dark mode renders properly
- [ ] Accessibility: proper ARIA, keyboard nav, contrast
- [ ] Showcase page created with all sections
- [ ] Navigation updated
- [ ] No duplicate components in the project
- [ ] Uses `cn()` for class merging
- [ ] Extends shadcn (not rebuilt from scratch)
- [ ] Props interface exported for TypeScript consumers

---

## Notes

- **shadcn MCP** is the preferred way to search and install components
- **CSS variables** are the source of truth (defined in `globals.css`)
- **Tailwind classes** reference CSS variables (`bg-primary`, `text-muted-foreground`)
- **Extend, don't rebuild** -- customize shadcn components, don't recreate them
- **components/ui/** is for shadcn base components (auto-generated, don't edit directly)
- **components/** root is for custom wrappers and new components
