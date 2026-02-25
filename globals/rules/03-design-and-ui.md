---
description: Design system, accessibility (a11y), and UI styling rules (Tactile Minimalism). Apply this rule when styling components, adding haptics, or implementing user interfaces.
globs: "*{.tsx,.jsx}"
---
# Design System: Tactile Minimalism & Usability

BEFORE styling any component, read `docs/02-DESIGN_SYSTEM.md`.

## Workflow Integration
- **When asked to build a new screen, hook, or feature**, you MUST follow the steps outlined in the `/feature-implementation.md` workflow to guarantee you are respecting the 4-Domain data boundaries and Zod validation rules.

## Accessibility (a11y) & Ergonomics
- **Semantic React Native**: Use semantic components (`Pressable`, `Text`, `View`, `Modal`) appropriately.
- **Screen Reader Support**: Every interactive element MUST be fully accessible. Any icon-only button MUST have an explicitly defined `accessibilityLabel`.
- **Target Areas (Invisible Hit Areas)**: Interactive elements must have a minimum clickable area of **48px x 48px** to accommodate touch interfaces. 
  - **Do NOT compromise aesthetic density** to achieve this.
  - **Use `hitSlop`**: For small visual elements (like a 24x24 icon button), use the `hitSlop` prop on `<Pressable>` (e.g., `hitSlop={{ top: 12, bottom: 12, left: 12, right: 12 }}`) to invisibly expand the clickable area without altering the visual layout.
- **Label Wrapping (Row Expansion)**: For form controls like checkboxes or switches, wrap the entire row (input + text) in a single `<Pressable>` so tapping the text toggles the input.

## Usability Best Practices
- **Explicit States**: Every interactive component must handle its states. In React Native, this means handling the `pressed` state (via NativeWind `active:` or `Pressable` render props) and the `disabled` state.
- **Disabled State Styling**: Disabled elements should have reduced opacity (e.g., `opacity-50`). You MUST prevent `onPress` handlers from firing if `disabled` is true.

## UI & Styling Rules (Tailwind v4 3-Tier Architecture)
- **CSS-First Architecture**: The app uses Tailwind v4 with a strict 3-tier CSS token system (`foundations.css` -> `tokens.css` -> `global.css`). 
- **NO RAW HEX OR PRIMITIVE COLORS**: Never hardcode hex values or use raw primitive palettes (like `bg-palette-neutral-900`) in components.
- **Consume Semantic Aliases ONLY**: UI components MUST exclusively use semantic aliases (e.g., `bg-surface-base`, `text-primary-emphasized`, `border-neutral-weak`). **Avoid name repetition** (e.g., use `text-primary-base` instead of `text-text-primary-base`).
- **Dark Mode via Data Attributes**: Rely strictly on the `[data-theme="dark"]` system managed in `tokens.css`. Never write inline `@media (prefers-color-scheme: dark)` or Javascript `Appearance.getColorScheme()` fallbacks in components.
- **Automated Design Check**: When editing or reviewing UI PRs, explicitly check that NO primitive palettes or raw hex codes are leaking into the `className` props. If a state cannot be achieved with existing Semantic Aliases, you must flag it for an architecture review before inventing a new variable.

## Typography
- **Visual Hierarchy**: Use the typography system strictly to establish visual order. Do not skip heading levels if it breaks logical document flow.

## Haptics and Animation
- Bind `expo-haptics` to interactive elements to simulate mechanical clicks.
- Avoid CSS gradients for buttons. Indicate pressed states by scaling down (`transform: scale(0.98)`) and adding borders.

### Examples

**BAD: Inaccessible, tiny touch target**
```tsx
// ❌ Visual size equals hit area (too small)
<Pressable onPress={deleteItem} className="w-5 h-5">
  <TrashIcon className="text-danger" />
</Pressable>
GOOD: hitSlop Expanded Hitbox (Preserves small visual size)

TypeScript
// ✅ Visual element is small, but hitSlop expands the clickable area to ~49x49px.
<Pressable 
  onPress={deleteItem} 
  accessibilityLabel={t('actions.delete_item')}
  hitSlop={{ top: 12, bottom: 12, left: 12, right: 12 }}
  className="items-center justify-center w-5 h-5 active:opacity-70"
>
  <TrashIcon className="w-full h-full text-neutral" />
</Pressable>
GOOD: Row-Expanded Hit Area

TypeScript
// ✅ Entire flex row is clickable, acting like an HTML <label>.
<Pressable 
  onPress={toggleTerms}
  accessibilityRole="checkbox"
  accessibilityState={{ checked: isAccepted }}
  className="flex-row items-center gap-2 p-2 rounded-md active:bg-surface-overlay"
>
  <View className={cn("w-4 h-4 rounded border", isAccepted ? "bg-action-primary" : "border-neutral")} />
  <Text className="text-body text-neutral">Accept Terms</Text>
</Pressable>
