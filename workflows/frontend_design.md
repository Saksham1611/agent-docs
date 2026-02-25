---
name: frontend-design
description: Create distinctive, production-grade frontend interfaces with high design quality. Use this skill when the user asks to build web components, pages, or applications. Generates creative, polished code that avoids generic AI aesthetics.
---

This skill guides creation of distinctive, production-grade frontend interfaces that avoid generic "AI slop" aesthetics. Implement real working code with exceptional attention to aesthetic details and creative choices.

The user provides frontend requirements: a component, page, application, or interface to build. They may include context about the purpose, audience, or technical constraints.

## Design Thinking

Before coding, understand the context and commit to a BOLD aesthetic direction:
- **Purpose**: What problem does this interface solve? Who uses it?
- **Tone**: Pick an extreme: brutally minimal, maximalist chaos, retro-futuristic, organic/natural, luxury/refined, playful/toy-like, editorial/magazine, brutalist/raw, art deco/geometric, soft/pastel, industrial/utilitarian, etc. There are so many flavors to choose from. Use these for inspiration but design one that is true to the aesthetic direction.
- **Constraints**: Technical requirements (framework, performance, accessibility).
- **Differentiation**: What makes this UNFORGETTABLE? What's the one thing someone will remember?

**CRITICAL**: Choose a clear conceptual direction and execute it with precision. Bold maximalism and refined minimalism both work - the key is intentionality, not intensity.

Then implement working code (HTML/CSS/JS, React, Vue, etc.) that is:
- Production-grade and functional
- Visually striking and memorable
- Cohesive with a clear aesthetic point-of-view
- Meticulously refined in every detail

## Frontend Aesthetics Guidelines

Focus on:
- **Typography**: Choose fonts that are beautiful, unique, and interesting. Avoid generic fonts like Arial and Inter; opt instead for distinctive choices that elevate the frontend's aesthetics; unexpected, characterful font choices. Pair a distinctive display font with a refined body font.
- **Color & Theme**: Commit to a cohesive aesthetic. Use CSS variables for consistency. Dominant colors with sharp accents outperform timid, evenly-distributed palettes.
- **Motion**: Use animations for effects and micro-interactions. Prioritize CSS-only solutions for HTML. Use Motion library for React when available. Focus on high-impact moments: one well-orchestrated page load with staggered reveals (animation-delay) creates more delight than scattered micro-interactions. Use scroll-triggering and hover states that surprise.
- **Spatial Composition**: Unexpected layouts. Asymmetry. Overlap. Diagonal flow. Grid-breaking elements. Generous negative space OR controlled density.
- **Backgrounds & Visual Details**: Create atmosphere and depth rather than defaulting to solid colors. Add contextual effects and textures that match the overall aesthetic. Apply creative forms like gradient meshes, noise textures, geometric patterns, layered transparencies, dramatic shadows, decorative borders, custom cursors, and grain overlays.

NEVER use generic AI-generated aesthetics like overused font families (Inter, Roboto, Arial, system fonts), cliched color schemes (particularly purple gradients on white backgrounds), predictable layouts and component patterns, and cookie-cutter design that lacks context-specific character.

Interpret creatively and make unexpected choices that feel genuinely designed for the context. No design should be the same. Vary between light and dark themes, different fonts, different aesthetics. NEVER converge on common choices (Space Grotesk, for example) across generations.

**IMPORTANT**: Match implementation complexity to the aesthetic vision. Maximalist designs need elaborate code with extensive animations and effects. Minimalist or refined designs need restraint, precision, and careful attention to spacing, typography, and subtle details. Elegance comes from executing the vision well.

Remember: Claude is capable of extraordinary creative work. Don't hold back, show what can truly be created when thinking outside the box and committing fully to a distinctive vision.

## Design Quality Checklist

Before shipping any screen or component, review against these dimensions:

| Dimension | Key Questions |
|---|---|
| **Visual Hierarchy** | Does the eye land where it should? Most important element = most prominent? Understandable in 2 seconds? |
| **Spacing & Rhythm** | Consistent and intentional whitespace? Elements breathe or cramped? Harmonious vertical rhythm? |
| **Typography** | Clear size hierarchy? Too many competing weights? Calm or chaotic? |
| **Color** | Used with restraint and purpose? Guides attention or scatters it? Sufficient contrast for accessibility? |
| **Alignment & Grid** | Consistent grid? Anything off by 1–2px? Every element locked into the layout with precision? |
| **Components** | Similar elements styled identically across screens? Interactive elements obvious? Hover/focus/disabled states accounted for? |
| **Iconography** | Consistent style, weight, and size? One cohesive set or mixed libraries? Support meaning or just decorate? |
| **Motion** | Natural and purposeful transitions? Motion that exists for no reason? Responsive to interaction? |
| **Empty States** | Intentional or broken when there's no data? User guided toward first action? |
| **Loading States** | Consistent skeletons/spinners/placeholders? App feels alive or frozen while waiting? |
| **Error States** | Consistently styled? Helpful and clear, or hostile and technical? |
| **Dark Mode** | Actually designed, or just inverted? Shadows and contrast ratios hold up? |
| **Density** | Anything removable without losing meaning? Every element earning its place? |
| **Responsiveness** | Works at mobile, tablet, and desktop? Touch targets sized for thumbs? Fluid adaptation, not just three breakpoints? |
| **Accessibility** | Keyboard navigation, focus states, ARIA labels, color contrast ratios, screen reader flow? |

## The Jobs Filter

Apply these to every element before finalizing:

- *"Would a user need to be told this exists?"* → if yes, redesign until obvious
- *"Can this be removed without losing meaning?"* → if yes, remove it
- *"Does this feel inevitable?"* → if no, it's not done
- *"Say no to 1,000 things"* → cut good ideas to keep great ones

## Design Rules

| Rule | Principle |
|---|---|
| **Simplicity** | Every element must justify its existence. Best interface = the one the user never notices. |
| **Consistency** | Same component = identical look and behavior everywhere. All values via design tokens. No hardcoded values. |
| **Hierarchy** | Every screen has one primary action — make it unmissable. If everything is bold, nothing is bold. |
| **Alignment** | Every element on a grid. No exceptions. Off by 1–2px = wrong. |
| **Whitespace** | Space is not empty — it is structure. When in doubt, add space, not elements. |
| **Feeling** | Premium interfaces feel calm, confident, and quiet. Transitions feel like physics, not decoration. |
| **Responsive** | Mobile first. Design for thumbs, then cursors. Intentional at every viewport. |
| **No cosmetic fixes without structural thinking** | "Make this blue" must explain what the color change accomplishes in the hierarchy. |

## States as Design

Empty, loading, and error states are not afterthoughts — they are first-class design surfaces:

- **Empty states**: Guide the user toward their first action. An empty state is a moment of opportunity, not a blank void.
- **Loading states**: Use consistent skeletons or placeholders. The app should feel alive, not frozen. Prefer skeleton screens over spinners for content-heavy layouts.
- **Error states**: Consistently styled, human in tone. Never expose raw technical errors. Always offer a path forward.

## Tech Stack Defaults (React)

When building React interfaces without explicit constraints:

- **Styling**: Tailwind CSS utility classes
- **Hooks**: React hooks for all state and effects
- **Icons**: Lucide React — do not install other icon libraries unless explicitly requested
- **Complex components**: Shadcn UI for forms, dialogs, dropdowns, and other interaction-heavy components — copy the component you need rather than importing the full library
- All designs must be beautiful, fully featured, and production-worthy — never cookie-cutter