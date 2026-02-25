---
name: tailwind-variants-slots
description: Complete guide for building and composing UI components using Tailwind Variants (v3+) with the slots pattern. Use when building complex React components that have multiple stylable elements.
---

# Tailwind Variants Slots Pattern

When building complex or multi-element UI components, ALWAYS use Tailwind Variants (TV) with the `slots` pattern instead of creating separate TV instances for every sub-element.

## Core Concepts

### 1. Basic Slot Usage
Define a single `tv` instance for the component, mapping all nested elements to a `slots` object.

```typescript
import { tv } from 'tailwind-variants';

const cardStyle = tv({
  slots: {
    base: 'bg-surface-base rounded-xl p-6 flex flex-col',
    header: 'flex items-center justify-between mb-4',
    title: 'text-text-neutral-base font-bold text-lg',
    description: 'text-text-neutral-weak text-sm',
  }
});

// Usage
export const Card = ({ title, description }) => {
  const { base, header, title, description } = cardStyle();
  return (
    <div className={base()}>
      <div className={header()}>
        <h3 className={title()}>{title}</h3>
      </div>
      <p className={description()}>{description}</p>
    </div>
  );
};
```

### 2. Slots with Variants
Apply variants to specific slots natively.

```typescript
const alertStyle = tv({
  slots: {
    base: 'p-4 rounded-md flex',
    icon: 'w-5 h-5 shrink-0',
    title: 'font-semibold',
  },
  variants: {
    intent: {
      success: {
        base: 'bg-action-success-soft',
        icon: 'text-action-success-base',
        title: 'text-action-success-emphasized',
      },
      danger: {
        base: 'bg-action-danger-soft',
        icon: 'text-action-danger-base',
        title: 'text-action-danger-emphasized',
      }
    }
  }
});
```

### 3. Compound Slots
If you need to apply the SAME class to multiple slots under certain conditions, use `compoundSlots`. This avoids repetition.

```typescript
const paginationStyle = tv({
  slots: {
    base: 'flex gap-1',
    item: 'bg-surface-base',
    prev: 'bg-surface-base',
    next: 'bg-surface-base',
  },
  variants: {
    size: {
      sm: {},
      md: {}
    }
  },
  compoundSlots: [
    {
      slots: ['item', 'prev', 'next'],
      size: 'sm',
      class: 'h-8 w-8 text-sm'
    },
    {
      slots: ['item', 'prev', 'next'],
      size: 'md',
      class: 'h-10 w-10 text-base'
    }
  ]
});
```

### 4. Compound Variants on Slots
If a specific variant combination requires you to alter multiple slots in strictly different ways, use `compoundVariants` and pass a class object targeting the slots.

```typescript
compoundVariants: [
  {
    intent: 'outlined',
    status: 'error',
    class: {
      base: 'border border-action-danger-base bg-transparent',
      title: 'text-action-danger-base',
    }
  }
]
```

### 5. Composing Components (`extend` API)
Never duplicate base UI variants. Inherit them using the `extend` prop, which automatically inherits variants, defaultVariants, and slots.

```typescript
const baseButton = tv({
  slots: {
    base: 'rounded-full px-4 py-2 font-medium',
    icon: 'w-4 h-4'
  }
});

const buyButton = tv({
  extend: baseButton,
  // Overriding/extending the existing slots
  slots: {
    base: 'bg-action-primary-base hover:opacity-80',
    label: 'uppercase tracking-widest' // Adding a new slot perfectly fine
  }
});
```

## Best Practices
1. **Never use single-element TVs when a component has children.** Always use the `slots` API.
2. **Abstract Layouts:** Keep layout styling (`flex`, `grid`, `m-*`) in the parent components wherever possible, or provide `className` overrides per slot.
3. **Class Merging:** Assume `tailwind-merge` runs automatically inside TV. No need to wrap slots in `cn()`.
4. **Overrides:** Allow consumers to override individual slots by accepting a `classNames` object prop mapped to the TV slots.
