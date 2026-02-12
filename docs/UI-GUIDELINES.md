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

### References

- [Google web.dev: High-performance CSS animations](https://web.dev/articles/animations-guide)
- [Google web.dev: Why are some animations slow?](https://web.dev/articles/animations-overview)
- [Nielsen Norman Group: Animation for Attention and Comprehension](https://www.nngroup.com/articles/animation-usability/)
- [Smashing Magazine: How Functional Animation Helps Improve UX](https://www.smashingmagazine.com/2017/01/how-functional-animation-helps-improve-user-experience/)
