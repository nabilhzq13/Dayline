# Dayline

A day planner for your phone that starts empty. Build your own timetable from
nothing, see the empty hours in your day and fill them, keep track of
assignments, exams and quizzes, and, if you like, your five daily prayers.
It has a calm, flat look in soft pastels, works with no signal, and keeps
everything on your phone. If you want, it can also keep a copy in a free
Supabase project of your own.

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

- **The Home button** sits at the bottom in the middle of every page. Tap it
  and your pages fan out above it in a half circle: Today, Week, Due, Solat (if
  it's on), Schedule and Settings. Tap one to go there. Tap Home again, tap
  anywhere else, or press Escape to fold them away. On a keyboard, Tab moves
  from Home into the pages and the arrow keys move between them.
- **Today** has a ring round each date of this week that fills as you tick that
  day's blocks, and the block you're in, with a countdown and **Start focus**.
  **Start focus** turns the screen into a big timer that keeps the phone awake.
  Below that is what's **Coming up**, your prayers if Solat is on, and then the
  day itself as a timetable: each block's start and end down the left, and a
  bar in its kind's colour. On a computer, the timetable and the rest sit side
  by side.
  - Tap the circle on a block to tick it, or swipe the block right.
  - Tap the block to open it: its picture, times and details, **Mark as done**,
    **Start focus** while it's on, and **Edit block**.
  - Swipe a block far left to edit it straight away.
- **Free time.** Your day runs from when you get up to when you go to bed
  (Settings, **Your day**). Any stretch of it of 15 minutes or more with no block
  shows as a dashed card, such as "Free · 1.5h". Each one offers up to two
  blocks to fill it: ones you have on other days first, then ideas for that time
  of day, like Breakfast, Study, Lunch, a walk, the gym, Dinner or a book. They
  are never prayers. Tap one to add it to that day, with an **Undo**.
  **Other…** opens the editor already set to that time and length.
- **Week** shows any day of the week as the same timetable, free time included,
  with a heatmap of the last eight weeks. Today has a dot under it. Tap a block
  to edit it.
- **Due** is for assignments, exams and quizzes. Tap **Assignment**, **Exam** or
  **Quiz** to add one: its name, the course, the date and time, notes, and files
  such as the brief (a PDF) or a photo of the whiteboard. Each kind has its own
  icon and colour, and the chips under the buttons show one kind at a time.
  - Every one says how it stands, **Upcoming**, **Due soon** (inside two days),
    **Overdue** or **Completed**, and how long is left. An exam or a quiz whose
    time has passed unticked shows as **Past** rather than overdue.
  - The next exam or quiz in the coming fortnight sits at the top with the days
    still to go.
  - Tap the circle when you've handed one in, or sat it. Today shows the next
    three that are coming up.
- **Solat**, if you turned it on, has the five prayers with JAKIM's official
  times for your zone. Tick each one once you've prayed it. A prayer whose time
  runs out unticked goes on your qadha list to make up.
- **Schedule** lists every block. Tap **Add** to add one. Two blocks can't share
  the same time on the same day. If a new one overlaps others, **Add and make
  room** shortens them, with an **Undo**.
- **Settings** is in the Home menu, and behind the gear at the top of every page.

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

Reminders put block starts, due dates, exams and quizzes (a day before and an
hour before) and prayer times on your lock screen while Dayline is closed. Your
own project sends them, so it needs a few more pieces.

Set them up on a computer, where you paste into Supabase. Something copied on a
phone can't be pasted on a computer. Open Dayline in the computer's browser,
connect the same Supabase and sign in to the same account, then open
**Settings**, then **Reminders**, then **Set up reminders in Supabase**:

1. **Make a key.** Dayline makes a key pair for your project. Copy both halves.
2. Run [`supabase/reminders.sql`](supabase/reminders.sql) in the SQL Editor. Copied
   from Dayline, it already has your project's address in it.
3. Under **Edge Functions**, deploy a new function **via the editor**. Name it
   `remind`, paste in [`supabase/functions/remind/index.ts`](supabase/functions/remind/index.ts),
   deploy it, then turn off **Verify JWT** in its settings.
4. Under **Edge Functions**, **Secrets**, add `VAPID_PUBLIC_KEY` and
   `VAPID_PRIVATE_KEY`.
5. On your iPhone, in Dayline from the home screen: **Settings**, **Reminders**,
   **Turn on reminders**, then **Send a test**.

Each Copy button has a **Show it** underneath. If a browser won't copy, the
text opens there, selected, to copy by hand.

Choose which kinds come, how early, and your quiet hours, during which nothing
comes. Reminders follow your phone's time zone.

Set reminders up before Dayline had exams and quizzes? Paste the function in
again (step 3) so theirs read "Exam tomorrow" rather than "is due tomorrow".

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
