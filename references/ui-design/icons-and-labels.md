# Icons and Text Labels

Use this whenever a UI shows an icon, a symbol, a status label, or a tag. It stops the generic AI look: text characters used as icons, one icon reused everywhere, and chips on every piece of text.

## Icons come from one source, and the user picks it

Settle the icon source before adding any icon:

1. **Check the project first.** Look in `package.json` and the existing components for an icon library (Material Symbols, Lucide, Phosphor, Tabler, Heroicons, Radix Icons, or a custom icon set or sprite in the repo). If one is there, use it and do not add another.
2. **If there is none, ask the user before installing or drawing anything.** Use `AskUserQuestion`. Offer reputable libraries that fit the stack, with your pick first marked "(Recommended)" (Material Symbols for Material 3 projects, Lucide for general Tailwind and React), plus an option for the user's own custom icons. Some projects prefer custom icons or one they already own, so never decide this yourself.
3. **Then install the chosen library as a package** (see `../package-installation/npm.md`) and import icons by name, or use the custom set the user points to.
4. Never hand-draw SVGs, paste random SVGs, or invent icon paths.
5. Use one library or set per project. Do not mix sources unless the user says so. Use one size scale, one stroke weight or fill style, and one corner style across the UI, and do not mix outlined and filled icons without a reason like selected vs not selected.
6. Brand logos (GitHub, Slack, Google) come from the brand's own assets or a brand-icon set, not from a generic icon.

## Never use text characters as icons

Do not use `->`, `→`, `+`, `-`, `x`, `✓`, `✕`, `>`, `...`, `★`, or emoji where an icon belongs. Use the library's arrow, plus, minus, close, check, chevron, and more icons. Text glyphs render differently per font and look unfinished.

## Every icon matches its label

- Choose the icon from the meaning of the text next to it, in this context. "Billing" gets a card or receipt, "Members" gets people, "Export" gets a download or share icon, "Delete" gets a trash can.
- Never use one icon for many things. Do not give every AI feature a sparkle, every feature a rocket, every list item a check, or every card a star or lightning bolt.
- If you cannot find an icon that clearly matches the label, use no icon. A label with no icon is better than a wrong or decorative one.
- Do not put an icon on everything. Add one only where it speeds up scanning: navigation items, actions, status, and empty states.
- Two different things never share the same icon on one screen, and one thing always uses the same icon.

## Accessibility

- An icon next to a visible text label is decorative: hide it from screen readers (`aria-hidden="true"`).
- An icon-only button needs an accessible name (`aria-label`) and a tooltip.
- Do not use colour alone to carry meaning; pair a status colour with an icon or text.

## Text labels: no chips by default

- Show a status, tag, or category as plain text. To give it emphasis, use a coloured text, a border colour, a small dot, or a custom treatment that fits the design.
- Do not wrap text in a pill, chip, or badge by default. Rows of rounded grey or tinted pills under every heading and card is the generic AI look.
- Use a chip or badge only when the user asks for it, or when it is a real control, such as a filter or selection chip the user can toggle, or a count on a nav item.
- When a chip is allowed, use the library's component with the project's tokens, and keep one style for all chips.
