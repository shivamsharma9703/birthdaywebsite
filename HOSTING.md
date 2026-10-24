# Vaishali's story — launch guide

## 1. Put it online (free): Vercel + Supabase

Packages are installed with **npm** (`package-lock.json`, `.npmrc`). Do not add a `bun.lock`; if one exists in your repo, delete it.

1. **GitHub** — replace the files in your repo with this project (keep your repo, commit, push).
2. **Supabase** (free) — create a project, open *SQL Editor*, paste the whole file
   `drizzle/migrations/0000_private_story_progress.sql`, run it. This creates her private progress table.
3. **Vercel** (free) — *Add New → Project → import the GitHub repo*. Leave the build settings as detected.
   Before the first deploy add these *Environment Variables*:

   | Name | Value |
   |---|---|
   | `ACCESS_CODE` | the word Vaishali types at the gate (you choose; not a date) |
   | `PREVIEW_PASSPHRASE` | your admin password for `/preview` (long, private) |
   | `SESSION_SECRET` | any random 40+ character string |
   | `SUPABASE_URL` | Supabase → Project Settings → API → Project URL |
   | `SUPABASE_SERVICE_ROLE_KEY` | Supabase → Project Settings → API → `service_role` key (keep secret!) |

4. Deploy. The build detects Vercel automatically (`vite.config.ts`).

## 2. Things only you can change

| What | Where |
|---|---|
| Your voice message (1–2 min, mp3) | `public/assets/audio/shivam-message.mp3` |
| Chapter ambience (optional) | `public/assets/audio/day01-room.mp3` … `day07-room.mp3` |
| Family names, Istanbul photo, extra photos | `src/lib/story/photos.ts` + `public/assets/photos` |

Missing audio is fine: the sound button simply doesn't appear.

## 3. Test the whole week before 1 November

Open `/preview`, enter your passphrase, set a date/time (e.g. `2026-11-05 18:00`), then walk the chapters on her
phone model. Preview never touches her saved progress. Tap **Exit preview** when done.

Unlock times (India time): 01–04 and 07 at midnight on their date; 05 at 6 AM and 06 at 6 PM on 5 November.

## 4. Run locally

```
bun install      # or npm install --legacy-peer-deps
ACCESS_CODE=word PREVIEW_PASSPHRASE=secret npm run dev
```
Locally (no Supabase variables) progress is saved to `.data/progress.json`. For a dry run of launch week add
`STORY_NOW_OVERRIDE=2026-11-06T09:00:00+05:30` (ignored in production builds).

## 5. iPhone / Safari notes

- Needs iOS 16.4 or newer (Settings → General → About → iOS Version).
- Open the link in **Safari**. If she taps it inside Gmail or WhatsApp it opens in that app's own browser, which keeps a separate
  login: she'd just enter the access word once more and her progress comes back.
- Safari → Share → **Add to Home Screen** makes it open like an app (full screen, with its own icon).
- Sound only starts after she taps; iPhones don't allow autoplay. The silent/ring switch can mute web audio, so check that
  the ringer isn't off.
