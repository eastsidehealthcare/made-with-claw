# UI Guidelines

Best practices for user interface design across Made With Claw sites.

## Animations

Animations can improve user engagement and perceived performance when used correctly. However, poorly implemented animations hurt SEO through Core Web Vitals penalties.

### When to Use Animation

**Do use animations for:**
- Visual feedback on user interactions (button hover/click states)
- Guiding attention to calls-to-action
- Smooth transitions between states (accordion open/close, modal appear)
- Scroll-triggered content reveals (subtle fade-in, once per element)
- Loading states and progress indicators

**Don't use animations for:**
- Gratuitous decoration without purpose
- Looping/infinite animations that distract
- Delayed content that makes users wait
- Every element on page load (overwhelming)
- Critical content that users need immediately

### Performance Rules

**Only animate these CSS properties** (GPU-accelerated, no layout impact):
- `transform` (translate, scale, rotate)
- `opacity`

**Never animate these properties** (triggers expensive layout/paint):
- `width`, `height`
- `margin`, `padding`
- `top`, `left`, `right`, `bottom`
- `font-size`
- `border-width`

### Implementation Guidelines

#### Timing
- **Micro-interactions** (hover, click): 100-200ms
- **Transitions** (page elements): 200-300ms
- **Larger movements** (modals, slides): 300-500ms
- Never exceed 500ms — users perceive delays beyond this

#### Easing
- Use `ease-out` for elements entering the viewport
- Use `ease-in` for elements leaving
- Use `ease-in-out` for state changes
- Avoid `linear` — feels mechanical/unnatural

#### Scroll Animations
```css
/* Fade-in on scroll - apply via JS when element enters viewport */
.animate-fade-in {
  opacity: 0;
  transform: translateY(20px);
  transition: opacity 0.4s ease-out, transform 0.4s ease-out;
}

.animate-fade-in.visible {
  opacity: 1;
  transform: translateY(0);
}
```

#### Hover States
```css
/* Button hover - subtle scale */
.btn {
  transition: transform 0.15s ease-out, box-shadow 0.15s ease-out;
}

.btn:hover {
  transform: translateY(-2px);
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
}

/* Card hover - lift effect */
.card {
  transition: transform 0.2s ease-out, box-shadow 0.2s ease-out;
}

.card:hover {
  transform: translateY(-4px);
  box-shadow: 0 8px 24px rgba(0, 0, 0, 0.12);
}
```

### Accessibility

**Always respect user preferences:**
```css
@media (prefers-reduced-motion: reduce) {
  *,
  *::before,
  *::after {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
  }
}
```

### Core Web Vitals Considerations

Animations affect these metrics:

| Metric | Risk | Mitigation |
|--------|------|------------|
| **CLS** (Cumulative Layout Shift) | Fly-in elements push content | Use `transform` only, reserve space |
| **LCP** (Largest Contentful Paint) | Heavy JS animation libraries | Use CSS animations, no libraries |
| **INP** (Interaction to Next Paint) | Janky animations block input | Keep animations under 100ms for interactions |

### Healthcare Site Considerations

For healthcare audiences (often older users seeking information quickly):

1. **Be conservative** — functionality over flash
2. **Subtle fade-ins** on scroll for content sections (once, not repeating)
3. **Clear hover states** on interactive elements
4. **No auto-playing animations** — respect user attention
5. **Fast transitions** — 200-300ms max

---

## Mobile Touch Targets

Touch interfaces require larger hit areas than desktop mouse interactions. Fingers are imprecise compared to cursor pointers.

### Minimum Touch Target Sizes

- **Minimum size:** 48x48px (Google's recommendation)
- **Comfortable size:** 48-56px height, full available width
- **Spacing between targets:** At least 8px to prevent mis-taps

### Mobile Navigation Menus

**Critical rule:** In mobile navigation menus, the clickable area should extend to:
- **Full width** of the menu container (not just the text width)
- **Full height** including the visual margin between menu items

**Wrong approach:**
```css
/* ❌ Only the text is clickable */
.nav-links a {
  padding: 8px 0;
}
```

**Correct approach:**
```css
/* ✅ Full touch target */
.nav-links a {
  display: flex;
  align-items: center;
  min-height: 48px;
  padding: var(--space-4) var(--space-6);
  margin: 0 calc(var(--space-6) * -1);  /* Extend to container edges */
  width: calc(100% + var(--space-6) * 2);
}
```

### Implementation Pattern

```css
/* Mobile menu with proper touch targets */
@media (max-width: 768px) {
  .nav-links {
    flex-direction: column;
    gap: 0;  /* Remove gap - let padding handle spacing */
    width: 100%;
  }

  .nav-links a {
    display: flex;
    align-items: center;
    min-height: 48px;
    padding: 16px 24px;
    margin-left: -24px;
    margin-right: -24px;
    width: calc(100% + 48px);
    border-bottom: 1px solid var(--color-border);
  }

  .nav-links a:active {
    background: var(--color-bg-secondary);  /* Visual feedback on tap */
  }
}
```

### Why This Matters

1. **Accessibility:** Users with motor impairments need larger targets
2. **Frustration reduction:** Mis-taps cause user frustration and abandonment
3. **Healthcare audiences:** Often older users with reduced fine motor control
4. **Speed:** Larger targets = faster navigation = better user experience

### References

- [Google Material Design: Touch Targets](https://m3.material.io/foundations/accessible-design/accessibility-basics#a9572d52-273e-457d-8293-bb57a5f4c6ce)
- [Apple HIG: Touch Targets](https://developer.apple.com/design/human-interface-guidelines/accessibility#Touch-targets)
- [WCAG 2.5.5: Target Size](https://www.w3.org/WAI/WCAG21/Understanding/target-size.html)

### References

- [Google web.dev: High-performance CSS animations](https://web.dev/articles/animations-guide)
- [Google web.dev: Why are some animations slow?](https://web.dev/articles/animations-overview)
- [Nielsen Norman Group: Animation for Attention and Comprehension](https://www.nngroup.com/articles/animation-usability/)
- [Smashing Magazine: How Functional Animation Helps Improve UX](https://www.smashingmagazine.com/2017/01/how-functional-animation-helps-improve-user-experience/)
