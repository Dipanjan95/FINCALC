## Summary

Implement a light/dark mode toggle with system preference support in the navigation bar. The project already has CSS variables for dark mode defined in `globals.css` but lacks the JavaScript functionality to toggle between themes.

## Environment

- **Repository**: https://github.com/Dipanjan95/FINCALC.git
- **Framework**: Next.js 15 (App Router)
- **UI Library**: shadcn/ui with Tailwind CSS v4
- **Current State**: Dark mode CSS variables exist but no toggle implementation

## Requirements

### Toggle Type
- **Dropdown menu** with three options:
  - ☀️ Light
  - 🌙 Dark
  - 🖥️ System (respects OS preference)

### Placement
- **Navigation bar (top right)** - alongside the existing calculator buttons

### Technical Implementation
1. Create a `ThemeProvider` using `next-themes` or similar library
2. Add a `ThemeToggle` component using shadcn/ui `DropdownMenu`
3. Integrate into the existing navigation in `src/app/page.tsx`
4. Persist user preference in localStorage
5. Respect system preference when "System" is selected
6. Prevent flash of wrong theme on page load

## Acceptance Criteria

- [ ] Dropdown menu appears in navbar with Light/Dark/System options
- [ ] Selecting "Light" forces light mode
- [ ] Selecting "Dark" forces dark mode
- [ ] Selecting "System" follows OS preference
- [ ] Preference persists across page reloads
- [ ] No flash of incorrect theme on initial load
- [ ] Works on all pages (home, mortgage, compound-interest)
- [ ] Uses existing shadcn/ui components (DropdownMenu, etc.)

## Implementation Notes

### Files to Modify/Create
- `src/components/theme-provider.tsx` - New: Theme provider wrapper
- `src/components/theme-toggle.tsx` - New: Dropdown toggle component
- `src/app/layout.tsx` - Wrap children with ThemeProvider
- `src/app/page.tsx` - Add ThemeToggle to navbar
- `src/app/mortgage/page.tsx` - Add ThemeToggle to navbar (if separate navbar)
- `src/app/compound-interest/page.tsx` - Add ThemeToggle to navbar (if separate navbar)

### Dependencies
- `next-themes` - For theme management (recommended)
- Or implement custom solution with `useEffect` and `localStorage`

### Shadcn/UI Components Needed
```bash
npx shadcn@latest add dropdown-menu
```

## Additional Context

The project uses:
- Tailwind CSS v4 with CSS variables for theming (defined in `globals.css` lines 7-76)
- shadcn/ui "base-nova" style
- `cssVariables: true` in components.json
- Custom variant for dark mode: `@custom-variant dark (&:is(.dark *));`

The dark mode class is applied to `.dark` selector, so the theme toggle needs to add/remove the `dark` class on the `<html>` element.

## Reproduction Steps (for testing)

1. Visit the site
2. Click the theme toggle in the navbar
3. Select "Dark" - page should switch to dark mode
4. Reload page - dark mode should persist
5. Select "System" - should follow OS preference
6. Change OS theme - site should update automatically