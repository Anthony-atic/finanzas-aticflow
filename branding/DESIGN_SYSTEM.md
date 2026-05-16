# ATICFLOW — Design System Rules

> **Source of truth for all UI decisions.** Read this before writing any frontend component.
> CSS tokens live in `apps/web/app/globals.css`. Brand assets in `branding/`.

---

## 1. Styling approach

**Inline styles with CSS custom properties.** NOT Tailwind utility classes.

```tsx
// CORRECT
<div style={{ background: "var(--surface-2)", border: "1px solid var(--line)", borderRadius: 14 }}>

// WRONG — no Tailwind classes for layout/color
<div className="bg-gray-900 border border-gray-700 rounded-xl">
```

Exception: utility classes defined in globals.css (`t-eyebrow`, `t-label`, `btn`, `card`, `pill`, etc.) are encouraged.

---

## 2. Colors (CSS vars)

| Token | Use |
|---|---|
| `--lime` / `--lime-dim` | Primary accent (CTA, active states, highlights) |
| `--lime-soft` / `--lime-soft-strong` | Lime backgrounds (pills, soft badges) |
| `--blue` / `--blue-soft` | Secondary accent, links |
| `--red` / `--red-soft` | Error, destructive |
| `--amber` / `--amber-soft` | Warning |
| `--bg` | Page background (#000 dark) |
| `--surface` | Elevated surface (#111) |
| `--surface-2` | Input/card inner (#161616) |
| `--surface-3` | Hover/secondary (#1C1C1C) |
| `--line` / `--line-strong` | Borders (7% / 14% white) |
| `--text` | Primary text (#FAFAFA) |
| `--text-2` | Secondary text (72% opacity) |
| `--text-3` | Tertiary/label text (46% opacity) |
| `--text-4` | Disabled/placeholder (28% opacity) |

---

## 3. Typography

| Class / var | Font | Use |
|---|---|---|
| `--font-display` (AICON) | Display | KPI numbers (`.t-num`), hero display-xl only |
| `--font-body` (LT Wave) | Body | All text, titles, headings |
| `--font-ui` (LT Wave UI) | UI | Buttons, nav labels |
| `--font-mono` (LT Wave Mono) | Mono | Labels, eyebrows, code, timestamps |

### Type utility classes

| Class | Spec |
|---|---|
| `.t-display-xl` | AICON 800, 56px, -0.03em |
| `.t-display-lg` | LT Wave 700, 32px, -0.022em |
| `.t-display-md` | LT Wave 700, 24px, -0.018em |
| `.t-display-sm` | LT Wave 700, 18px, -0.012em |
| `.t-label` | Mono 500, 11px, 0.08em, uppercase, text-3 |
| `.t-eyebrow` | Mono 500, 10px, 0.12em, uppercase, text-3 |
| `.t-mono` | Mono, tnum+ss01 |
| `.t-num` | AICON 800, tnum, -0.02em |

---

## 4. Surfaces & containers

| Element | How to use |
|---|---|
| `.card` | Liquid glass material. Primary container. Use for forms, panels, sections. |
| `.card-2` | Flat surface-2 bg + line border. Nested cards, secondary containers. |
| `.divider` | 1px horizontal rule `var(--line)` |
| `.vdivider` | 1px vertical rule |
| `.hatch` | Diagonal hatch pattern (45deg, `--hatch` color) |
| `.hatch-lime` | Lime-tinted hatch |

---

## 5. Inputs

Standard input pattern (inline styles):

```tsx
const inputStyle: React.CSSProperties = {
  width: "100%",
  background: "var(--surface-2)",
  border: "1px solid var(--line)",
  borderRadius: 10,
  padding: "8px 12px",
  color: "var(--text)",
  fontSize: 13,
  fontFamily: "var(--font-body)",
  outline: "none",
  height: 40,
  boxSizing: "border-box",
  transition: "border-color 160ms var(--ease)",
};
```

Or use the `.input` class (height 36, radius `--r-sm`, focus → lime border).

Labels above inputs: `<div className="t-eyebrow" style={{ marginBottom: 6 }}>Label *</div>`

---

## 6. Buttons

| Class combo | Use |
|---|---|
| `btn btn-primary` | Lime bg, black text. Main CTA. |
| `btn btn-secondary` | Surface-3 bg, line border. Secondary action. |
| `btn btn-ghost` | Transparent, text-2. Tertiary action. |
| `btn btn-icon` | 36x36 circle, surface-3 bg. Icon-only. |
| `btn-sm` | 28px height, 12px font |
| `btn-lg` | 44px height, 14px font |

---

## 7. Pills / badges

| Class | Appearance |
|---|---|
| `.pill` | Default: surface-3, mono 11px |
| `.pill-lime` | Lime bg, black text |
| `.pill-blue` | Blue-soft bg, blue text |
| `.pill-red` | Red-soft bg, red text |
| `.pill-amber` | Amber-soft bg, amber text |
| `.pill-dot` | Adds 6px dot before text |

---

## 8. Radius tokens

| Token | Value |
|---|---|
| `--r-xs` | 8px |
| `--r-sm` | 12px |
| `--r-md` | 16px |
| `--r-lg` | 20px |
| `--r-xl` | 24px (`.card` default) |
| `--r-pill` | 999px (buttons, pills) |

---

## 9. Layout tokens

| Token | Value |
|---|---|
| `--sidebar-w` | 240px |
| `--topbar-h` | 56px |
| `--pad` | 24px (16px in compact density) |
| `--pad-tight` | 16px (12px in compact) |

---

## 10. Motion

| Token | Value |
|---|---|
| `--ease` | `cubic-bezier(0.32, 0.72, 0.24, 1)` |
| `--ease-out` | `cubic-bezier(0.16, 1, 0.3, 1)` |

All transitions: 120-160ms duration.

---

## 11. Page layout pattern

```tsx
<div style={{ padding: "28px 32px", maxWidth: 720, margin: "0 auto" }}>
  <div className="t-eyebrow" style={{ marginBottom: 4, color: "var(--text-3)" }}>
    SECTION · CONTEXT
  </div>
  <h1 className="t-display-lg" style={{ margin: 0 }}>Page Title</h1>
  <p style={{ fontSize: 13.5, color: "var(--text-3)", marginTop: 8 }}>
    Subtitle description.
  </p>

  <div className="card" style={{ padding: 28, marginTop: 22 }}>
    {/* content */}
  </div>
</div>
```

---

## 12. Section headers inside cards

```tsx
<div style={{ display: "flex", alignItems: "center", gap: 8, marginBottom: 18 }}>
  <Icon size={15} style={{ color: "var(--text-3)" }} />
  <span className="t-label">Section Name</span>
</div>
```

---

## 13. Error states

```tsx
<div className="t-mono" style={{
  fontSize: 12,
  color: "var(--red)",
  padding: "10px 14px",
  background: "var(--red-soft)",
  borderRadius: 10,
  border: "1px solid rgba(239, 68, 68, 0.20)",
}}>
  {error}
</div>
```

---

## 14. Success states

Lime icon + lime text for header. Agent/entity pills use `surface-2` bg + `line` border.

---

## 15. Dark/Light mode

All tokens auto-switch via `[data-theme="light"]` overrides in globals.css. Use CSS vars — never hardcode hex colors.
