---
description: how to build new UI components using Tailwind Variants and slots
---

# Workflow: Creating UI Components with TV Slots

When tasked with creating a new complex UI component (a card, list item, navigation bar, advanced button), follow these steps strictly to guarantee the correct architecture.

1. **Analyze the UI Structure:**
   Identify all DOM/Native nodes that will compose the component. Mentally map these to slot keys (e.g., `base`, `iconWrapper`, `title`, `descriptionActionRow`).

2. **Initialize the TV Instance (with Slots):**
   At the top of the file (outside the component render function), declare the `tv({})` configuration using the `slots` API. Do NOT write `base:` configuration at the root of the TV instance if you have multiple elements. Put it inside `slots: { base: '...' }`.

3. **Declare Variants & Default Variants:**
   Map out your states (e.g., `intent`, `size`, `isDisabled`). Write stylistic impacts on each specific slot inside the variant block. Ensure you define a `defaultVariants` mapping.

4. **Implement Compounds (If Necessary):**
   - If a variant changes multiple slots with the exact same utility classes, use `compoundSlots`.
   - If different variants in combination (e.g., `intent="primary" && isDisabled=true`) change specific slots, use `compoundVariants`.

5. **Expose the Component Interface:**
   - Consume the TV instance inside the React component using destructuring: `const { base, title } = myComponent({ ...variants });`
   - Pass the strings to `className`.
   - Ensure you allow the consumer to pass standard `className` (applied to the `base` slot) and a custom `classNames` object (applied to overriding inner slots).

6. **Validate against Design Tokens:**
   Always remember to cross-reference the project's CSS tokens (e.g., `bg-surface-base`, `text-text-primary-base`). Never inject raw hex codes or Tailwind palette primitives.
