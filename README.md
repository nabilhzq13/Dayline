# Dayline

A day planner for your phone that starts empty. Build your own timetable from
nothing, see the empty hours in your day and fill them, keep track of
assignments and their due dates, and, if you like, your five daily prayers.
It has a warm Liquid Glass look, works with no signal, and keeps everything on
your phone. If you want, it can also keep a copy in a free Supabase project of
your own.

**Open it:** https://nabilhzq13.github.io/Dayline/

## Putting it on your iPhone

1. Open the link above in **Safari**.
2. Tap **Share**, then **Add to Home Screen**, then **Add**.
3. Open Dayline from your home screen. The welcome walks you through it:
   your name, when your day starts and ends, prayer times if you want them,
   and a timetable to start from. You can also start with a blank week.

It works the same in any browser on a computer or an Android phone. Only the
home-screen app on an iPhone can get reminders, because that's the one place
iOS lets a web app have them.

## Using it

- **Today** has a ring for each day of this week that fills as you tick that
  day's blocks, and the block you're in, with a countdown and **Start focus**.
  **Start focus** turns the screen into a big timer that keeps the phone awake.
  Below that are what's **Due soon**, your prayers if Solat is on, and then the
  day itself as cards, each in its kind's colour.
  - Tap the circle on a card to tick it, or swipe the card right.
  - Tap the card to open it: its picture, times and details, **Mark as done**,
    **Start focus** while it's on, and **Edit block**.
  - Swipe a card far left to edit it straight away.
- **Free time.** Your day runs from when you get up to when you go to bed
  (Settings, **Your day**). Any stretch of it of 15 minutes or more with no block
  shows as a dashed card, such as "Free · 1.5h". Each one offers up to two
  blocks to fill it: ones you have on other days first, then ideas for that time
  of day, like Breakfast, Study, Lunch, a walk, the gym, Dinner or a book. They
  are never prayers. Tap one to add it to that day, with an **Undo**.
  **Other…** opens the editor already set to that time and length.
- **Week** shows any day of the week as the same cards, free time included,
  with a heatmap of the last eight weeks. Tap a block to edit it.
- **Due** is for assignments and anything else with a deadline. Tap **+** to add
  one: what's due, the course, the date and time, notes, and files such as
  the brief (a PDF) or a photo of the whiteboard. They're listed soonest first,
  with overdue ones at the top, and each shows how long is left. Tap the circle
  when you've handed one in. Today shows the next three.
- **Solat**, if you turned it on, has the five prayers with JAKIM's official
  times for your zone. Tick each one once you've prayed it. A prayer whose time
  runs out unticked goes on your qadha list to make up.
- **Schedule** lists every block. Tap **+** to add one. Two blocks can't share the
  same time on the same day. If a new one overlaps others, **Add and make room**
  shortens them, with an **Undo**. The gear opens **Settings**.

## Your own Supabase (optional)

Without it, everything stays on your phone and you back up with a file (below).
With it, a copy of everything, files included, lives in a free
[Supabase](https://supabase.com) project that belongs to you. A lost phone gets it all back, and a
second phone stays in step. Nobody else can see it, not even Dayline: there is
no Dayline server.

In Dayline, open **Settings**, then **Your own Supabase**, then **Set it up**.
Doing it on a computer is easiest. The steps:

1. Make a free project at supabase.com.
2. In its **SQL Editor**, run [`supabase/setup.sql`](supabase/setup.sql). Dayline
   has a **Copy the SQL** button. This makes a private table and a private file
   store that only your account can read.
3. Under **Authentication**, **Sign In / Providers**, **Email**, turn off
   **Confirm email**. You can also leave it on and confirm from the email
   Supabase sends you.
4. Copy the **Project URL** and the **publishable** (or **anon public**) key into
   Dayline and tap **Connect**.
5. Make your account with an email and a password. From then on it syncs by
   itself, and whichever copy changed last wins.

## Reminders (optional, needs your own Supabase)

Reminders put block starts, due dates (a day before and an hour before) and
prayer times on your lock screen while Dayline is closed. Your own project
sends them, so it needs a few more pieces. In the home-screen app, open
**Settings**, then **Reminders**, then **Set up reminders in Supabase**:

1. **Make a key.** Dayline makes a key pair for your project. Copy both halves.
2. Run [`supabase/reminders.sql`](supabase/reminders.sql) in the SQL Editor. Copied
   from Dayline, it already has your project's address in it.
3. Under **Edge Functions**, deploy a new function **via the editor**. Name it
   `remind`, paste in [`supabase/functions/remind/index.ts`](supabase/functions/remind/index.ts),
   deploy it, then turn off **Verify JWT** in its settings.
4. Under **Edge Functions**, **Secrets**, add `VAPID_PUBLIC_KEY` and
   `VAPID_PRIVATE_KEY`.
5. Tap **Turn on reminders**, then **Send a test**.

Choose which kinds come, how early, and your quiet hours, during which nothing
comes. Reminders follow your phone's time zone.

## Backups

**Settings**, **Backup file**: **Back up to iCloud** saves one file with
everything, attachments included. Choose **Save to Files**, then
**iCloud Drive**. **Restore from file** brings it back, here or on a new phone,
and the welcome screen offers it too. Today asks for a fresh backup once a week,
unless your own Supabase is keeping a copy.

## What Dayline sends, and where

Apart from backups you make yourself, Dayline sends only three things: your sync
copy to your own Supabase while you're signed in, this phone's push address
while reminders are on, and your zone code to JAKIM for prayer times.

## Files

- `index.html` — the whole app: one file, with no build step and no libraries.
- `sw.js` — keeps Dayline working offline, and shows reminders.
- `manifest.webmanifest`, `icon-*.png` — the home-screen app and its icon.
- `fonts/` — Inter, self-hosted (SIL Open Font License, see `fonts/OFL.txt`).
- `supabase/` — the SQL and the reminder function for your own project.

## Changing the app

Edit `index.html`, then raise the number in `CACHE` in `sw.js` (`dayline-v1`
becomes `dayline-v2`), so phones pick up the new version. To try it on a
computer first, run `python -m http.server` in this folder and open
http://localhost:8000. Dayline keeps its data under its own names (`dl.*`),
so it never mixes with other apps on the same address.

## Credits

Built from [Break](https://github.com/nabilhzq13/TimetableNabuzy), its owner's
personal timetable. The illustrations are drawn for Dayline. The typeface is
Inter by Rasmus Andersson. Prayer times come from JAKIM's e-Solat.
