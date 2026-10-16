# Pixel Android UI

Use this for Android app UI, Material You, Material 3 Expressive visuals, or a web mockup of an Android screen. Read `material-design-3.md` first. For ordinary web UI with a Pixel-inspired look, use `material-3-web.md` instead.

## Official references

General Material Design 3 links are in `material-design-3.md`. Android-specific references:

- Android design: https://developer.android.com/design
- Material Design for Android: https://developer.android.com/develop/ui/views/theming/look-and-feel

If the task needs exact Android component behavior, platform tokens, or latest Pixel-specific behavior, check the official Android and Material docs.

## Visual direction

Pixel Android UI should feel:

- Soft and tactile.
- Rounded and spacious.
- Colorful but controlled.
- System-driven, not custom-themed from scratch.
- Friendly, expressive, and easy to touch.

Prefer:

- Large rounded containers.
- Pill-shaped buttons and segmented controls.
- Dynamic color-inspired palettes.
- Soft surface tinting, combined with container color instead of relying only on shadows for elevation.
- Clear selected states.
- Big, readable labels.
- Icon + label navigation when space allows.
- Motion that feels responsive and physical.

Avoid:

- Sharp enterprise-style rectangles everywhere.
- Dense desktop-first tables for mobile flows.
- Random gradients unrelated to the Material color system.
- Tiny touch targets.
- Hidden states with no visual feedback.

## Android-first layout patterns

Use these patterns when they match the app:

- Bottom navigation for top-level mobile destinations.
- Navigation rail for tablet, foldable, or wider Android layouts.
- App bars for screen identity, navigation, and important actions.
- Large cards or containers for grouped content.
- Floating action button for the primary creation action.
- Modal bottom sheets for focused secondary actions.
- Segmented buttons for mutually exclusive modes.
- Toolbars for frequent editing actions.
- Split buttons when a primary action has related alternatives.

## Expressive component style

Material 3 Expressive-style UI can use:

- Larger shapes.
- More obvious selected states.
- Playful but controlled motion.
- Stronger color containers.
- Button groups that visually connect related actions.
- Progress indicators with more personality, when appropriate.
- Toolbars with rounded grouped controls.

Keep expressive styling purposeful. Use it to improve discoverability, feedback, and hierarchy.

## Pixel-style examples

Toolbar:

```text
rounded container
  selected icon button
  icon button
  icon button
  icon button
```

Split action:

```text
[ icon + Primary action ][ chevron ]
```

Button group:

```text
[ Selected ][ Option ][ Option ]
```

Navigation:

```text
compact phone: bottom navigation
wide/tablet: navigation rail
```

## Implementation checklist

- Use Material components before custom controls.
- Use dynamic color-like roles: primary, secondary, tertiary, surface, container, on-color.
- Keep text readable and touch targets comfortable.
- Cover the full state checklist in `components.md`, with especially clear selected states.
- Use Android navigation patterns before desktop navigation patterns.
- For web mockups that imitate Pixel UI, preserve Android proportions and touch-friendly spacing.
