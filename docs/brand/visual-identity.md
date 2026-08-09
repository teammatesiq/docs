---
Document title: TeamMatesIQ Visual Identity Standard
Version: 1.0
Status: Current
Owner: Head of Brand
Last updated: 2026-08-09
Decision status: Approved; Flow Path v1 is the canonical production identity; legal and trademark availability review remains outstanding
---

# 1. Purpose

This document defines the approved visual identity for TeamMatesIQ and TeamMates SME v1. It governs colour, typography, imagery, the Flow device, brand-lockup architecture and the canonical Flow Path v1 production assets.

Flow Path v1 was approved for canonical publication on 2026-08-09. Implementations must still validate accessibility in their actual context. Legal and trademark availability review remains outstanding and may require controlled remediation through brand change control.

# 2. Creative Territory: The Flow

**The Flow** represents work moving smoothly between people and their digital teammates so capacity opens up.

The signature device is a distinctive flowing ribbon or pathway connecting tasks, people and outcomes. It must improve recognition or comprehension and must not become decorative clutter.

# 3. Colour System

| Token | Name | Hex | Primary role |
|---|---|---|---|
| `brand.navy` | Deep Navy | `#0B1F3A` | Brand foundation, dark surfaces and confident emphasis. |
| `brand.blue` | Clear Blue | `#2563EB` | Primary action, links and ribbon identity. |
| `brand.aqua` | Aqua | `#20B8A6` | Flow accent and controlled role highlights. |
| `surface.warm` | Soft White | `#F7F8F5` | Warm page and content backgrounds. |
| `neutral.slate` | Slate | `#475569` | Secondary text and interface neutrals. |
| `text.ink` | Ink | `#142033` | Primary text on light surfaces. |

## 3.1 Usage rules

- Deep Navy should provide confidence without making every surface dark.
- Clear Blue anchors primary actions and key interactive elements.
- Aqua is an accent and must not be used for small text on light backgrounds.
- Soft White should introduce warmth and reduce a clinical software feel.
- Dark brand-led hero areas should transition into lighter content sections for clarity.
- Status, warning, error and success colours are product-semantic tokens and must not be inferred from this brand palette.

All final colour combinations and interaction states must meet WCAG 2.2 AA requirements.

# 4. Typography

| Use | Typeface | Fallback |
|---|---|---|
| Brand headings | Manrope | Arial, sans-serif |
| Body copy | Inter | Arial, sans-serif |
| Product interface | Inter | Arial, sans-serif |

Typography should feel confident, modern, warm and clear. Product usability and legibility take precedence over decorative treatment.

# 5. Brand-Lockup Architecture

| Level | Treatment |
|---|---|
| Corporate brand | TeamMatesIQ primary logo. |
| Product | TeamMates wordmark, endorsed with **by TeamMatesIQ** where context requires. |
| Individual roles | Admin TeamMate and future role names as product titles, not separate logos. |
| Compact mark | Refined ribbon-and-IQ symbol. |
| App icon and favicon | Symbol-only version designed and tested specifically for small sizes. |

Future roles may use controlled accent colours or identifiers within the shared identity. They must not introduce unrelated logos, typefaces or colour systems.

**Helping businesses work smarter.** is the TeamMatesIQ brand promise. It is not part of the logo or primary brand lockup and must not be incorporated into either.

# 6. Approved Logo: Flow Path v1

Flow Path v1 is the approved production identity. It refines the ribbon-and-IQ concept into two forward-moving ribbons that express movement, continuity and opened capacity.

The approved asset family includes:

- TeamMatesIQ corporate lockups in primary, reversed and single-colour treatments
- TeamMates endorsed product lockups in primary and reversed treatments
- colour, navy and white standalone symbols
- light and navy application icons
- favicon variants tested down to 16 px
- outlined wordmarks that do not depend on an installed font
- flat approved colours with no gradients

Admin TeamMate, Project TeamMate and future role names remain product titles and must not receive separate logos.

SVG is the canonical master format. PNG files are convenience derivatives and should be regenerated from the SVG masters when another size is required.

Production assets and usage guidance are held at [`assets/brand/flow-path/v1/`](../../assets/brand/flow-path/v1/README.md).

# 7. Imagery

Use:

- real people in authentic SME settings
- recognisable work and practical outcomes
- calm, confident compositions
- product imagery that shows useful work, review and control
- warmth balanced with professional clarity

Avoid:

- robots, androids or artificial people
- circuit boards, glowing brains and neural-network clichés
- futuristic or science-fiction aesthetics
- generic smiling-at-a-laptop stock photography
- visuals suggesting unrestricted access or uncontrolled autonomy
- effects that reduce legibility or accessibility

# 8. Iconography and Product Imagery

- Use simple, consistent icons that support comprehension.
- Do not use robot heads, magic wands or sparkles as default AI shorthand.
- Use screenshots and product mock-ups only when they represent released or clearly labelled preview behaviour.
- Show evidence, approval and status in a way that reinforces customer control.

# 9. Accessibility and Quality Control

Implementations using the production assets must be checked for:

- WCAG 2.2 AA contrast
- keyboard-focus visibility where interactive
- legibility at supported responsive sizes
- meaningful alternative text
- reduced-motion handling for animated Flow treatments
- file size and rendering performance
- correct clear space, minimum size and background use

# 10. Asset Status

Flow Path v1 is the canonical TeamMatesIQ and TeamMates production identity. Its master files, digital exports, proof and usage rules are approved and versioned under [`assets/brand/flow-path/v1/`](../../assets/brand/flow-path/v1/README.md).

The approval covers the artwork and usage system. It does not close the legal and trademark availability review, and it does not remove the requirement to validate contrast, legibility, file performance and alternative text in each implementation context.

# 11. Related Documents

- [Brand Foundation](brand-foundation.md)
- [Messaging Architecture](messaging-architecture.md)
- [Brand Decision Log](brand-decision-log.md)
- [Admin TeamMate UX/UI Specification](../ux/admin-teammate-ux-ui-specification.md)
