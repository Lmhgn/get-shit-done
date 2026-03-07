# O2 Empire — Email Template Reference

## Files
| File | Purpose |
|------|---------|
| `email-template-events.html` | Main HTML template (paste into SF) |
| `email-template-events.txt` | Plain-text fallback (deliverability) |

## Merge Tags / AMPscript Variables

Replace every `%%TAG%%` with your Salesforce field or AMPscript variable.

| Tag | Replace with |
|-----|-------------|
| `%%FIRST_NAME%%` | Contact first name field |
| `%%EVENT_1_TICKET_URL%%` | Ticket link for featured event |
| `%%EVENT_2_NAME%%` | Name of event 2 |
| `%%EVENT_2_DATE%%` | Date string e.g. "Fri 22 Aug 2025" |
| `%%EVENT_2_DESCRIPTION%%` | Short blurb (1–2 sentences) |
| `%%EVENT_2_PRICE%%` | Price string e.g. "From £15" |
| `%%EVENT_2_TICKET_URL%%` | Ticket link |
| *(repeat pattern for EVENT_3, EVENT_4)* | — |
| `%%LAST_CHANCE_EVENT%%` | Name of urgency event |
| `%%LAST_CHANCE_URL%%` | Ticket link for urgency strip |
| `%%ALL_EVENTS_URL%%` | Link to full events listing page |
| `%%OPTIN_SOURCE%%` | Where contact subscribed |
| `%%UNSUBSCRIBE_URL%%` | SF unsubscribe link |
| `%%PREFERENCES_URL%%` | SF preference centre link |

## Layout Structure

```
┌──────────────────────────────┐
│  HEADER  (gradient + logo)   │
├──────────────────────────────┤
│  INTRO personalisation line  │
├──────────────────────────────┤
│  EVENT 1 — Hero card (full)  │  ← Large featured show
├──────────┬───────────────────┤
│ EVENT 2  │ EVENT 3           │  ← 2-up grid (stack mobile)
├──────────┴───────────────────┤
│  EVENT 4 — Wide landscape    │  ← Image left / text right
├──────────────────────────────┤
│  URGENCY STRIP (last chance) │
├──────────────────────────────┤
│  SEE ALL EVENTS CTA          │
├──────────────────────────────┤
│  FOOTER                      │
└──────────────────────────────┘
```

## Colour System

| Role | Hex |
|------|-----|
| Background | `#0a0a0f` |
| Card surface | `#12121e` |
| Brand blue (dark) | `#1400ff` |
| Brand blue (light) | `#0070ff` |
| Accent red (badges) | `#ff3b5c` |
| Body text | `#9999bb` |
| Heading text | `#ffffff` |

## Salesforce Setup

1. **Marketing Cloud**: Use Content Builder → Code Snippet. Paste HTML into the HTML pane and the .txt content into the Text pane.
2. **Pardot**: Use the Email Template builder in HML mode. Swap `%%TAG%%` syntax for `{{recipient.firstName}}` Handlebars style.
3. **Data Extension**: Create a DE with columns matching your event fields, then use AMPscript `Lookup()` to pull per-subscriber event data.

## Image Guidelines

- Featured card image: **620 × 360px** minimum, `object-fit: cover`
- Grid card images: **400 × 220px** minimum
- Landscape card image: **400 × 240px** minimum
- Host on CDN (Cloudinary, Imgix, or SF Content Builder) — avoid email attachments

## Figma

To port this to Figma:
1. Use **Auto Layout** frames mirroring the table structure above
2. Apply `Inter` or `DM Sans` for closest web match to Helvetica Neue
3. Use component variants for the three card types (Hero / Grid / Landscape)
4. Export frame at 2× for handoff; map colours to a shared style library
