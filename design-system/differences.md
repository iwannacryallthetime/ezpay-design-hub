# Prototypes vs design system: old → new

Where the AI checker and the requestor form differ from `tokens.css` and `components.css`.
Nothing in the prototypes has been changed yet; use this table to decide what to fix.

**Where:** **C** = AI checker, **R** = requestor form, **C+R** = both.

**Applies everywhere:** both prototypes reference palette steps directly in their CSS (`var(--slate-200)`,
`var(--teal-700)` …). In the design system, components use only semantic aliases (`--border`, `--accent` …).
The rows below call out the specific cases.

## Tokens

| Where | Old | New | What differs |
|---|---|---|---|
| C+R | `--radius` | `--radius-lg` | Renamed. Same 8px |
| C | `4px` hardcoded (39 times) | `--radius-sm` | The requestor form already uses `--radius-sm` in places |
| C+R | `6px` radius (total banner, toast) | `--radius-md` | New token |
| R | `50%` / `9px` radius (stepper dot, switch) | `--radius-full` | New token |
| C+R | `--mono` | `--font-mono` | Renamed |
| C+R | `--shadow-xs` | `--shadow-xs` | Same |
| C+R | `0 1px 1px rgba(0,0,0,.05)` | `--shadow-row` | Hardcoded today |
| C+R | `6px 0 16px rgba(2,17,37,.04)` | `--shadow-sidebar` | Hardcoded today |
| C+R | `0 4px 2px rgba(0,0,0,.1)` | `--shadow-pressed` | Hardcoded today |
| C+R | `0 20px 25px -5px rgba(0,0,0,.15)` | `--shadow-dialog` | Hardcoded today |
| C+R | Document page double shadow | `--shadow-sheet` | Hardcoded today |
| C+R | `#fff` (28 to 31 times) | `--surface`, `--text-inverse`, `--text-on-brand` | Hardcoded today |
| C+R | `#000` (page title, collapse button) | `--text-heading` (= `--nav-text` #0e1114) | Snapped; ΔE 5.4 |
| C+R | `#087a65` (primary button hover) | `--action-primary-hover` (= teal-700) | Snapped; same lightness, slightly bluer, ΔE 8.6 |
| C+R | `#2b3648` (viewer toolbar) | `--doc-toolbar-bg` (= slate-700) | Snapped; ΔE 4.9, slightly lighter |
| C+R | `#525659` (viewer canvas) | `--doc-canvas-bg` (= new `--doc-grey`) | Kept as a new token; nothing close |
| C+R | `#eef1f4` (workspace switch) | `--sidebar-switch-bg` (= slate-100) | Snapped; ΔE 1.5 |
| C+R | `#f5f5f5` (brand chip) | `--sidebar-brand-chip-bg` (= slate-50) | Snapped; ΔE 2.0 |
| C+R | `#09090b` (signed-in name) | `--sidebar-user-name` (= nav-text) | Snapped; ΔE 2.8 |
| C+R | `#71717a` (staff number) | `--sidebar-user-meta` (= slate-500) | Snapped; same lightness, ΔE 9.8 |
| C+R | `rgba(97,108,118,.49)` (inactive workspace) | `--sidebar-switch-inactive` (= slate-400) | Solid instead of translucent |
| C+R | `rgba(15,23,42,.4)` (dialog backdrop) | `--backdrop` | Same colour via `color-mix` |
| C+R | `rgba(248,250,252,.4/.5/.8)` (card header, file row, claim side) | `--surface-subtle` | Solid instead of translucent |
| C+R | `rgba(240,253,250,.5/.9)` (item header, selected file) | `--surface-selected` | Solid instead of translucent |
| C+R | `rgba(15,118,110,.1)` + `rgba(13,148,136,.2)` (total pill) | `--accent-softer` + `--border-accent` | Solid tokens |
| C+R | `rgba(15,118,110,.8)` / `rgba(204,251,241,.9)` (total banner) | `--border-on-brand` / `--text-on-brand-muted` | Solid tokens |
| C+R | `rgba(0,0,0,.06)` (icon button hover) | `--surface-muted` | Solid token |
| C | `rgba(254,242,242,.4)`, `rgba(255,251,235,.7)`, `rgba(253,230,138,.7)` | `--error-bg-subtle`, `--warning-bg-subtle`, `--warning-bg` | Solid status tokens |
| C+R | Font sizes 9px (badges, file type) | `--font-size-2xs` (10px) | 1px larger |
| C | Font sizes 8px, 18px, 24px | (not in scale) | Only the mock invoice and sidebar workspace switch use them |
| C+R | Line heights 13.5, 16.5, 17.88, 19.5px | Scale pairs (14, 16, 18, 20px) | Rounded to the scale |
| C+R | `letter-spacing` on uppercase labels | none | Only needed for all-caps |
| C+R | 10px spacing (28 lines: 13 in C, 15 in R) | `--space-2` (8px), or `--size-row` / `--size-header` | Gaps and control padding move to 8px; row heights come from size tokens |
| C+R | Paddings 9, 11, 13, 17px | `--space-*` + 1px border | Figma's "step + border" values |

## Text case

| Where | Old | New | What differs |
|---|---|---|---|
| C | `text-transform: uppercase` on section titles, field labels, attachment headings, banner label, AI panel title, AI section titles, discrepancy headings, comments label, banner pill, LIVE | Sentence case | All-caps removed |
| C | "Review Required", "Re-run Line Check", "Total Amount", "Fund Center:", "Tax Code" | "Review required", "Re-run line check", "Total amount", "Fund centre:", "Tax code" | Title Case → sentence case; also British "centre" |
| C+R | Sidebar: "Checking Tasks", "New C. Requests", "My Requests", "Supporting tasks", "New Advance", "My Advance", "User Guide", "My Feedback" | "Checking tasks", "New C. requests", "My requests" … | Title Case → sentence case |
| C | Tab "Details (AI-Enabled) ✨" | "Details (AI-enabled)" | Sentence case |

## Buttons

| Where | Old | New | What differs |
|---|---|---|---|
| C+R | `.btn-verify` | `.btn.btn-primary` | Neutral name (it's also "Submit claim"); hover colour token |
| C+R | `.btn-outline` | `.btn.btn-secondary` | C has no hover style; R tints teal-50 on hover |
| C+R | `.btn-reject` | `.btn.btn-danger` | Neither prototype has a hover style; DS adds one |
| C+R | `.btn-plain` | `.btn.btn-plain` | Adds hover |
| C | `.btn-teal`, `.btn-teal.sm` | `.btn.btn-accent`, `.btn-sm` | Renamed |
| C+R | `.link-btn` | `.btn-link` | C: 11px / weight 500. R: 12px / weight 600. DS: 12px / 600 |
| C | `.rerun`, `.undo` | `.btn-link` | Separate one-off styles today |
| C+R | `.icon-btn` | `.btn-icon` | R turns red on hover for every icon button; DS hover is neutral |
| R | `.icon-btn` on file remove | `.btn-icon.btn-icon-danger` | Red hover only where the action removes something |
| C+R | `.item-close` | `.btn-icon` | Separate style today |
| R | `.btn-remove` | `.btn-link.btn-link-danger` | Renamed |
| R | `.add-item` | `.btn-add` | Renamed; adds disabled state |
| C+R | (none) | `:disabled` on every button | Neither prototype styles disabled buttons |

## Badges and status tags

| Where | Old | New | What differs |
|---|---|---|---|
| C+R | `.sec-num` | `.num-badge` | Renamed |
| C+R | `.strip-num` | `.num-badge.num-badge-solid` | Renamed |
| C+R | `.chip` | `.chip` | Same |
| C+R | `.tag-teal` | `.badge.badge-accent` | Renamed |
| C | `.tag-review` | `.tag.tag-warning` + alert icon | No icon today |
| C | `.tag-ready` | `.tag.tag-success` + check icon | No icon today |
| C | `.badge.fail / .pass / .na / .ai / .resolved` | `.badge-error / -success / -neutral / -ai / -success` + icon | **Colour only today**; DS pairs each with an icon |
| C | `.count-fail`, `.count-ok` | `.badge.badge-xs.badge-error / -success` + icon | Colour only today |
| R | `.lr-status.missing / .err / .ai / .ok` | `.badge-warning / -error / -ai / -success` + icon | Text only today; DS adds an icon |
| R | `.ai-tag` | `.badge.badge-ai.badge-xs` | Renamed |
| C | `.live` ("LIVE") | `.badge-live` ("Live") | Uppercase text |
| C+R | `.pdf` | `.filetype` (`.filetype-solid` in the viewer tab) | R uppercases with CSS; C hardcodes "PDF" |
| C+R | `.total-pill` | `.summary-pill` | Translucent colours → tokens |
| C | `.ai-dot`, `.ai-dot.warn` | `.status.status-success / -warning` | Renamed |
| R | `.rv-receipt`, `.rv-receipt.none` | `.status.status-success / -warning` | Renamed |
| C | `.ai-banner .pill` ("Action needed", "Ready") | `.badge.badge-xs.badge-warning / -success` | Uppercased by CSS; one-off style |

## Form fields

| Where | Old | New | What differs |
|---|---|---|---|
| C+R | `.f-label` | `.field-label` | C: 11px slate-400 uppercase. R: 12px slate-500 |
| C+R | `.f-value` | `.field-value` | C lays out with an icon; R wraps long values |
| R | `.f-error` | `.field-error` + alert icon | No icon today |
| C+R | `.field` | `.field` (+ `.field-grid` for aligned rows) | C stacks with flex; R uses subgrid to align. DS: flex by default, subgrid inside `.field-grid` |
| C+R | `.fields` | `.field-grid` | Renamed |
| R | `.input` | `.input` | Adds disabled; padding 10px → 8px |
| C | `.comments input`, `.dlg textarea` | `.input`, `textarea.input` | One-off styles today |
| R | `.affix-wrap`, `.affix` | `.input-affix`, `.affix` | Renamed |
| R | `.lt-search` | `.input-search` | Renamed |
| C+R | `.filter`, `.filters` | `.filter-chip`, `.filter-chips` | **Different in each**: C has no border, slate selected, 11px; R has a teal selected state, 12px. DS follows R |
| R | `.switch` | `.switch` | Same; adds disabled |
| R | `.dropzone`, `.dropzone.over` | `.dropzone`, `.dropzone.is-over` | Error state on the box instead of its card |

## Cards and section headers

| Where | Old | New | What differs |
|---|---|---|---|
| C+R | `.card` | `.card` | Same |
| C+R | `.card-head` | `.card-header` | Translucent background; padding 10/11px → min-height token |
| C+R | `.sec-title` | `.section-title` | C: 12px uppercase. R: 13px |
| C+R | `.card-meta` | `.card-meta` | Same |
| C+R | `.items-head` | `.list-header` | Renamed |
| C | `.item-strip` | `.item-header` | Renamed |
| R | `.line-strip` | `.item-header` | Renamed |
| C | `.item-summary` | `.item-row` | C shows rows at 75% opacity until hover; 12-column grid |
| R | `.line-row` (+ `.lr-*`), review `.item-summary` | `.item-row` | Renamed |
| C+R | `.item-open` | `.item-card` | Renamed |
| R | `.line` (open line in step 1) | `.item-card` | 1px border + teal shadow vs 2px border |
| R | `.line-foot` | `.item-footer` | Renamed |
| C+R | `.box`, `.amount-box`, `.desc-box`, `.coding-box` | `.box`, `.key-value` | Coding box becomes a key/value list |
| R | `.ck-card`, `.checklist`, `.ck` | `.card` + `.checklist`, `.checklist-item` | Renamed |
| C | `.placeholder-panel` | `.empty-state` | Renamed |
| R | `.att-box` | `.card` | Attachment boxes are plain cards |

## Navigation

| Where | Old | New | What differs |
|---|---|---|---|
| C+R | `.page-head` | `.page-header` | Padding differs between the two |
| C | `.tabs`, `.tab` | `.tabs`, `.tab` | Adds hover and disabled |
| R | `.stepper`, `.step`, `li.done` | `.stepper`, `.step`, `li.is-done` | State class renamed |
| C+R | `.sidebar` | `.sidebar` | Same structure; colours now tokens |
| C+R | `.brand`, `.brand-word`, `.brand-chip` | `.sidebar-brand`, `.word`, `.chip` | Renamed |
| C+R | `.role-switch`, `.role` | `.workspace-switch`, `.workspace-option` | Renamed |
| C+R | `.nav-link`, `.nav-sub` | `.nav-link`, `.nav-link.is-sub` | Padding 10px → 40px min-height |
| C+R | `.nav-me` | `.nav-user` | Renamed |
| C+R | `.collapse-btn` | `.sidebar-collapse` | Renamed |
| C+R | `.actionbar` | `.action-bar` | Renamed |
| C+R | `.decisions`, `.decision-hint` | `.action-bar-group`, `.action-bar-hint` | Gap 10px → 8px |

## Files and the document viewer

| Where | Old | New | What differs |
|---|---|---|---|
| C | `button.file[aria-pressed]` | `.file-row[aria-pressed]` | Renamed |
| R | `div.file` + `.file-open` + `.file-actions`, selected via `.viewing` | `.file-row` | **Structure differs**: R wraps a button inside a div to fit Replace/remove; DS uses `aria-pressed` for selected |
| R | `.rv-file-btn` | `.file-row` | Renamed |
| C+R | `.file-name`, `.file-sub`, `.file-end` | `.name`, `.meta`, `.end` | Renamed |
| C+R | `.doc`, `.doc-tab`, `.doc-toolbar`, `.doc-canvas` | `.doc-viewer`, `-tab`, `-toolbar`, `-canvas` | Renamed |
| C+R | `.sheet` | `.doc-viewer-page` | C's mock invoice sheet |
| C+R | `.no-preview` | `.doc-viewer-empty` | C: slate-500 text; R: slate-300 with an icon |
| C+R | `.total-banner` | `.total-banner` | Label uppercase in C |

## Dialogs and toasts

| Where | Old | New | What differs |
|---|---|---|---|
| C+R | `dialog` + `.dlg` | `dialog.dialog` + `.dialog-body` | Renamed |
| C+R | `.dlg-actions` | `.dialog-actions` | Renamed |
| C+R | `.dlg .err` | `.field-error` | Shared error style |
| C+R | `.toast.show` | `.toast.is-floating.is-visible` | State class renamed |

## AI checker patterns

| Where | Old | New | What differs |
|---|---|---|---|
| C | `.ai-head` | `.ai-panel-header` | Title uppercase today |
| C | `.ai-banner.warn / .ok` | `.ai-banner.ai-banner-warning / -success` | Renamed |
| C | `.panel`, `.panel.a / .b` | `.ai-section`, `.ai-section.is-tinted` | Renamed |
| C | `.panel-toggle`, `.panel-title`, `.panel-body` | `.ai-section-toggle`, `.title`, `.ai-section-body` | Title uppercase today |
| C | `.cmp-row`, `.cmp-flag`, `.cmp-resolved` | `.compare-row`, `.compare-flag`, `.compare-resolved` | Renamed |
| C | `.check`, `.check.fail / .resolved`, `.check-row`, `.check-detail` | `.check-item`, `.is-fail / .is-resolved`, `.check-row`, `.check-detail` | Renamed |
| C | `.discrepancy`, `.low-conf` | `.discrepancy`, `.low-confidence` | Headings uppercase today |
| C | `.comments`, `.saved-note` | `.comment-bar`, `.note` | Renamed |

## Only in one prototype, not in the design system

Left out on purpose; add them if they come up again.

- **C:** mock invoice and email sheets (`.inv-*`, `.email-*`, `.guest`, `.paid`), highlight (`.hl`).
- **R:** `.gst-note`, `.other-cur`, `.tpl-actions` (template picker), `.ck-progress`, `.lr-*` sub-parts covered by `.item-row`.
