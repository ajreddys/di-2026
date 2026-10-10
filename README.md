# Pharmakaksha · UPSC Drug Inspector batch

A one-page brochure for Pharmakaksha's batch for the UPSC Drug Inspector (CDSCO) recruitment under Advertisement No. 07/2026, to be served at <https://di26.pharmakaksha.com>. It is a single static `index.html` in the ed-tech app design used for gpat27.pharmakaksha.com, recoloured teal, with no build step. Fonts load from Google Fonts. Everything else is inline.

## What's on the page

| Section | What it shows |
| --- | --- |
| App bar and hero | Logo, Register button, a "Registrations open till …" badge, the headline and a countdown to the next date |
| Quick stats | 186 posts, Level 8 pay, Group B Gazetted, lowest batch fee |
| Dates | UPSC's application window (closed 17 Jul 2026), our batch dates, and the Recruitment Test and interview marked "Awaited from UPSC". Status chips are worked out in IST |
| Posts | Vacancies by category, the 8 PwBD posts by disability group and suitability, the duties under Rules 51 and 52, and service details |
| Eligibility | Qualification, citizenship, upper age limits with relaxations, UPSC fee |
| Selection | A 4-step stepper (apply → shortlist → interview → appointment), minimum interview marks, other ways UPSC may shortlist, what to bring to the interview |
| Inside the batch | Daily tests, weekly tests, 5 full-length mocks, Drugs & Cosmetics Act focus, notes, one-to-one |
| What we cover | Six accordions of Pharmakaksha's own coverage. The advertisement has no test syllabus |
| Study plan | Progress card and one card per week, then mocks and the test (built from `PLAN`) |
| Pricing | Day 1 free card, Individual (promo code with Copy) and Group prices, contact buttons |
| Footer and sticky bar | Social links, source and disclaimer; "n days to …" with Share and Register |

After `regClose`, the badge says registrations are closed, the free-trial card hides, and the Register buttons change to "Ask about the next batch", linking to WhatsApp chat.

There is no score calculator or guessing guide, because UPSC hasn't published the test's pattern or marking. Add them from the GPAT page once it does.

## Editing

Everything you'll usually change is at the bottom of the `<script>` in `index.html`.

### `CONFIG`

| Key | Meaning |
| --- | --- |
| `fee`, `code`, `codeOff` | Standard fee, promo code, ₹ off with the code |
| `groupMin`, `groupOff` | Group size and ₹ off per person (doesn't combine with the code) |
| `regClose` | When registrations close, as an ISO time with `+05:30` |
| `batchStart` | Text shown above Pricing |
| `exam` | The Recruitment Test start time once UPSC announces it, e.g. `"2027-02-14T09:30:00+05:30"`. While it's `""`, the page says "Awaited from UPSC". Once it's set, the countdown and the test card use it |
| `mocks` | Number of full-length mocks shown on the plan |
| `planDraft` | `true` shows a "Draft" chip on the study plan. Set it to `false` once the plan is final |
| `whatsapp`, `chat`, `email`, `register`, `url` | Links. They are also written into the HTML, so they work without JavaScript. If you change one, change both places |
| `shareText` | WhatsApp share message (the page URL is added after it) |
| `cfAnalyticsToken` | Cloudflare Web Analytics token. It loads only on di26.pharmakaksha.com. `""` (the current value) turns it off |

### `MILESTONES` and `PLAN`

`MILESTONES` holds the dates the countdown runs to, each `{ at, label, short }`. The test is added automatically from `CONFIG.exam`.

`PLAN` has one entry per row: `{ phase }` for a label, `{ week, from, to, topics, practice }` for a Monday-to-Sunday week (`free: true` on week 1), `{ mocks: true, from, note }` and `{ exam: true }`.

### Dates and facts in the HTML

The batch dates (2 Nov, 8 Nov) also appear in the dates timeline, the plan heading, the `<head>` preview tags and the share text. Update those along with `CONFIG`. When UPSC announces the Recruitment Test, update the timeline, the Selection section and the plan note, then bump the `?v=` on `og:image`.

## Share images

- `og-image.jpg` (1200×630) is the link preview. Its source is `marketing/src/og-image.html`.
- `marketing/whatsapp-status-1080x1920.jpg` is a WhatsApp status. Its source is `marketing/src/whatsapp-status.html`.

Both repeat numbers from `CONFIG`. If you change them, edit the HTML sources, then re-render from the repository root (needs Google Chrome on macOS):

```sh
sh marketing/src/render.sh
```

## Deploy

GitHub Pages, via `.github/workflows/deploy.yml`. Every push to `main` publishes only `index.html`, `logo.jpg`, `CNAME`, `.nojekyll` and `og-image.jpg`.

1. Create a public repository on GitHub, for example `ajreddys/di-2026`, and push this folder to `main`.
2. In the repository, go to **Settings → Pages** and set **Source = GitHub Actions**.
3. At your DNS provider, add a record: Type `CNAME`, Host `di26`, Value `ajreddys.github.io`.
4. In **Settings → Pages**, enter `di26.pharmakaksha.com` as the custom domain. Once the DNS check passes, tick **Enforce HTTPS**.

## Files

| File | Purpose |
| --- | --- |
| `index.html` | The page |
| `logo.jpg` | Logo and favicon |
| `og-image.jpg` | Link preview image |
| `CNAME`, `.nojekyll` | Pages domain and no Jekyll processing |
| `.github/workflows/deploy.yml` | Pages deploy |
| `marketing/src/` | HTML sources and `render.sh` for the share images |
| `marketing/whatsapp-status-1080x1920.jpg` | WhatsApp status image (not deployed) |

## Source

Post details come from UPSC Advertisement No. 07/2026, Item 52 (Vacancy No. 26060752127): 186 posts (UR 55, EWS 41, OBC 39, SC 35, ST 16; PwBD 8), Level 8, Group B Gazetted, B.Pharm or equivalent, age 30 for UR/EWS with the usual relaxations, applications 27 Jun – 17 Jul 2026. The study plan and the "What we cover" list are Pharmakaksha's own, not a UPSC syllabus. Pharmakaksha is not affiliated with UPSC, CDSCO or the Government of India.
