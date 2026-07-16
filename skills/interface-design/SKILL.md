---
name: interface-design
description: Guidance for distinctive, intentional interface design across web, mobile, tablet, and desktop applications. Use when creating, implementing, or substantially reshaping user interfaces, design systems, screens, flows, dashboards, landing pages, or app shells; when choosing visual direction, typography, color, layout, navigation, interaction, motion, and product copy; or when adapting one product identity across platforms without producing templated UI.
---

# Interface Design

Act as the design lead at a small studio known for giving every product a visual identity that could not be mistaken for anyone else's. Make deliberate, opinionated choices specific to the brief. Take one real aesthetic or interaction risk that can be justified by the subject, then execute it with restraint.

## Establish the design context

Before designing, identify:

- the concrete product or subject;
- its audience and their context of use;
- the interface's single primary job;
- the target platforms and form factors;
- the expected inputs: touch, pointer, keyboard, stylus, remote, or a combination;
- technical, brand, accessibility, and design-system constraints.

If the brief leaves the subject, audience, primary job, or platform ambiguous, make a defensible choice and state it briefly. Use known user preferences and existing project context as evidence, but do not invent requirements that conflict with the brief.

For an existing product, inspect the current implementation, assets, content, and design language before proposing a new direction. Preserve useful conventions intentionally; do not redesign merely to leave a mark.

## Ground the identity in the subject

Find the visual and interaction language inside the subject's own world: its materials, instruments, artifacts, environments, workflows, history, and vocabulary. Use real or realistic domain content throughout. Distinctiveness should emerge from what the product is, not from decoration applied after the layout is finished.

Choose one signature element the interface will be remembered by. It may be a spatial idea, typographic behaviour, navigation mechanism, data representation, transition, illustration system, or tactile interaction. It must embody the brief and help the experience rather than merely attract attention.

## Design principles

### Make the opening state a thesis

The first meaningful state should express what is characteristic about the product:

- On the web, this may be a hero, live demonstration, editorial opening, or immediate utility.
- On mobile, it is often the first useful screen, primary action, or content object rather than a marketing composition.
- On desktop, it may be the primary workspace, document, canvas, timeline, or command surface.

Do not default to a large headline, supporting paragraph, two buttons, three statistics, and a gradient accent. Use that composition only when it is truly the clearest expression of the brief.

### Let typography carry personality

Pair typefaces deliberately across display, body, and utility roles. Choose them for the subject, language coverage, platform rendering, legibility, and available weights—not because they are fashionable defaults. Define an intentional type scale, line length, weight, width, spacing, and hierarchy. Support text scaling and avoid layouts that break when type grows.

### Make structure mean something

Navigation, panes, hierarchy, grouping, labels, dividers, numbering, cards, and density must encode relationships that are true of the content. Number items only when order matters. Use cards only when containment or independent action is meaningful. Do not turn every section into a floating rounded rectangle.

### Design interaction as part of the identity

Choose how the interface feels to operate: direct or guided, calm or kinetic, dense or spacious, continuous or stepwise. Use motion for orientation, causality, hierarchy, and feedback. Prefer one orchestrated moment over scattered effects. Respect reduced-motion settings and never make animation necessary to understand or complete a task.

### Match complexity to the vision

Maximalist directions require layered, coherent execution. Minimal directions require exceptional precision in spacing, typography, alignment, states, and rhythm. Complexity is not quality; fidelity to a clear idea is.

## Respect each platform

Keep a shared product identity while adapting behaviour to platform expectations. Do not stretch a phone layout across a desktop window or shrink a desktop workspace onto a phone.

### Web

- Design fluidly for content and viewport changes, not only a few fixed device screenshots.
- Support keyboard, pointer, and touch where relevant; treat hover as an enhancement, never the only path.
- Preserve browser expectations such as links, history, focus, scrolling, zoom, and text reflow.
- Account for loading performance, long and localized content, narrow viewports, and very wide screens.

### Mobile and tablet

- Prioritize touch, reachability, clear targets, safe areas, system bars, virtual keyboards, rotation, and interruption.
- Respect platform navigation and gesture conventions unless there is a strong, tested reason to depart.
- Design for dynamic type, permissions, connectivity changes, loading, and recovery.
- Use larger tablet space to improve hierarchy or parallelism; do not merely enlarge the phone layout.

### Desktop

- Design for resizable windows, high information density, precise pointer input, keyboard workflows, and multi-window use.
- Provide sensible focus order, shortcuts, menus, context actions, selection behaviour, and undo where the task warrants them.
- Adapt panes and toolbars as space changes. Define useful minimum, comfortable, and expansive window states.
- Keep frequent actions efficient without hiding important capabilities behind mobile-style navigation.

### Cross-platform products

Keep the conceptual model, terminology, content hierarchy, core task flow, and signature identity consistent. Adapt navigation placement, density, controls, windowing, and input behaviour per platform. Reuse tokens and semantics where they improve coherence; do not force identical components where native expectations differ.

## Avoid unearned defaults

Current generated interfaces often cluster around a few familiar solutions: warm cream with a high-contrast serif and terracotta accent; near-black with one acid accent; broadsheet grids with hairline rules; blue-purple gradients; glass panels; oversized metrics; universal pill shapes; icon-in-a-coloured-square feature lists; and dashboards made entirely of a sidebar plus interchangeable KPI cards.

All are valid when supported by the brief. None is a substitute for a direction. Where the brief fixes an axis, follow it exactly. Where it leaves freedom, spend that freedom on a choice derived from the subject rather than one of these defaults.

## Process: understand, explore, critique, build, inspect

Work in two broad passes.

### 1. Form a compact design plan

Define:

- **Context:** subject, audience, primary job, platforms, form factors, and input methods.
- **Direction:** one sentence describing the intended character and the subject-specific reason for it.
- **Color:** four to six named hex values with semantic roles and dark/high-contrast variants when required.
- **Type:** at least two roles, with explicit scale, weights, widths, and fallback strategy.
- **System:** spacing, shape, borders, elevation, iconography, imagery, and motion rules.
- **Structure:** navigation, content hierarchy, responsive or adaptive behaviour, and concise layout sketches for each target platform.
- **Signature:** the one memorable element and why it belongs.
- **States:** loading, empty, error, success, disabled, selected, offline, and permission states that the flow needs.

Prefer one strong direction over a menu of weak options unless the user asks to compare concepts.

### 2. Critique before building

Test every choice against the brief:

- Could this palette, type pairing, layout, or signature be dropped unchanged into an unrelated product?
- Does each structural device communicate a real relationship?
- Is the platform adaptation genuine or merely a resize?
- Is the risk helping identity or usability?
- Is any decorative element competing with the primary job?

Revise generic or unsupported choices before implementation. Keep most internal iteration private; show the user only decisions that help them evaluate the direction.

### 3. Build from the revised plan

- Follow the chosen tokens and direction consistently.
- Fit the existing technology and component architecture unless a change is necessary.
- Use semantic tokens and reusable primitives without abstracting one-off ideas prematurely.
- Watch style precedence and overrides so component, variant, state, and platform rules do not silently cancel one another.
- Use real interface copy and realistic data rather than lorem ipsum or generic feature claims.
- Implement all required interaction states, not only the ideal screenshot.

### 4. Inspect the rendered result

Render or run the interface and inspect it visually. Capture screenshots when the environment permits. Check representative viewport or window sizes, text scaling, long content, empty and error states, and the relevant input methods. Verify keyboard focus, assistive labels and semantics, contrast, target sizing, and reduced motion.

Critique the implementation against the plan, fix discrepancies, then remove one unnecessary accessory before finishing.

## Write interface copy as design material

Write from the user's side of the screen. Name things by what people recognize and control, not by the system's architecture. A person manages notifications, not webhook configuration.

- Prefer plain, specific language over slogans or cleverness.
- Use active voice and make controls describe their result: “Save changes,” not “Submit.”
- Keep action vocabulary consistent through the flow: “Publish” should lead to “Published.”
- Let labels label and examples demonstrate; do not make one phrase do several jobs.
- Explain failures with the cause and a recovery path. Do not apologize or use vague errors.
- Make empty states direct the next useful action.
- Match the register to the product and audience while keeping sentence case and concise phrasing.

## Quality floor

Do not announce these as extras; include them as part of competent design:

- accessibility across visual, motor, auditory, and cognitive needs;
- clear focus and selection states;
- keyboard access where the platform supports it;
- screen-reader names, roles, values, and logical reading order;
- sufficient contrast and non-color cues;
- appropriate touch and pointer targets;
- text scaling, localization tolerance, and content reflow;
- reduced motion and alternatives to gesture-only actions;
- responsive or adaptive behaviour across supported sizes;
- useful loading, empty, error, offline, permission, and recovery states.

Spend boldness in one place. Keep everything around the signature element quiet, coherent, and useful.
