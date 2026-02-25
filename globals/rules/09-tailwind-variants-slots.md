---
description: Tailwind Variants (TV) formatting guidelines. Apply this whenever you create or modify UI components.
globs: "*{.tsx,.jsx}"
---

# UI Components: Tailwind Variants (Slots Pattern)

Whenever building or refactoring UI components, you **MUST** strictly adhere to the Tailwind Variants (TV) `slots` pattern as your styling paradigm.

## Rules:
1. **Never write raw Tailwind class strings in DOM/Native nodes** for multi-element components. Abstract them into a `tv({ slots: { ... } })` configuration block outside the render function.
2. **Never create multiple separate `tv()` instances** for a single React component (e.g., `const buttonBase = tv(); const buttonIcon = tv();`). Instead, map them to a single instance using the `slots` object (e.g., `slots: { base: '', icon: '' }`).
3. **Use `compoundSlots`** to apply classes to multiple slot elements simultaneously based on variants (e.g., applying specific width/height constants to all `['prev', 'next', 'item']` slots when `size: 'sm'`).
4. **Component Composition:** When building on top of base elements (e.g., extending a BaseCard into a ProfileCard), you MUST use the TV `extend` prop (`const profileCard = tv({ extend: baseCard, ... })`) rather than manually merging classes.
5. **ClassName Prop Architecture:** When exporting reusable components, allow slot overrides by accepting an optional `classNames` object prop that matches the slot keys, allowing consumers to override specific underlying DOM nodes easily.

### Example (ClassNames Override Pattern):
```tsx
const cardTV = tv({ slots: { base: 'border', body: 'p-4' } });

export const Card = ({ children, className, classNames }) => {
  const { base, body } = cardTV();
  return (
    // 'className' acts as the wrapper override, 'classNames' for internal slots
    <div className={base({ class: [className, classNames?.base] })}>
      <div className={body({ class: classNames?.body })}>
        {children}
      </div>
    </div>
  );
};
```
