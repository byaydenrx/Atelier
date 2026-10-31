# Atelier

A personal studio app for iPhone, built for one freelance designer's commission business. Atelier keeps projects, clients, Square invoices, money and mail in one place, and puts project due dates on the calendar.

SwiftUI and SwiftData, with a home-screen widget, in a black, monochrome Liquid Glass design.

> **About this repository.** Atelier is a private app, made for one person's workflow, and its source code isn't published. This repository documents what it does, how it's put together and the decisions behind it. There's nothing here to build or download.

## Why it exists

Commission work was spread over several apps: payments in Square, conversations in email, due dates on a list. Answering "who still owes me?" meant cross-checking all of them.

Atelier brings that together. Square stays the source of truth for clients and money, mail stays on the mail server, and due dates go to the calendar you already look at.

## What's in it

Today · Projects · Clients · Invoices · Finance · Mail, with Search on the side. You can reorder or hide tabs and the sections on Today.

| Tab | What it shows |
| --- | --- |
| **Today** | A dashboard of widgets you arrange yourself (see below) |
| **Projects** | Every commission with its client, business, price, what's owed, status (Not Started, In Progress, Waiting, Ready, Completed) and its invoice's status |
| **Clients** | Square customers, their businesses and Instagram handles, active and past projects, total owed. A **Top** filter ranks clients by what they've paid. Any project can be attached to a client by hand |
| **Invoices** | Square invoices with status and balance; write a new one without leaving the app |
| **Finance** | Income and expenses by day, week, month or year, with history and what's still expected. Tap a bar in the chart to see that day's numbers. Square's processing fees are kept apart from expenses, with their own list and total |
| **Mail** | One or more IMAP/SMTP accounts: read, reply, compose, archive, delete |
| **Search** | One box across everything, ranked so names that start with what you typed come first |

## Today

Today is a grid of widgets, each small (half width) or wide. Hold a widget for its menu, then **Edit Today**: the widgets shake like the Home Screen, and you can drag them into a new order, resize them, remove them, or add more from a gallery. Presets fill Today in one tap: At a Glance, Project Focus, Money Focus, Weekly Review and Minimal.

The widgets:

- **Essentials:** income overview with quick actions, quick-create buttons, a daily summary (due, overdue, money in today, next event, unread mail).
- **Projects:** due today, overdue, needs attention, upcoming deadlines, waiting on clients, awaiting payment, ready to deliver, recently updated, active project cards, and a workload chart by status.
- **Money:** income today, this week and this month; outstanding invoices; expected income; a monthly goal with progress; this week against last week; a business health check (income pace, overdue work and invoices, waiting clients, what's due); recent transactions and recent expenses.
- **Schedule and mail:** a month calendar of due dates, upcoming events, unread mail.

The header can show a time-of-day greeting, your own greeting, or none, and the date in full, short, or not at all. **Screen privacy** hides every amount in the app, for showing your screen to someone or working in public.

## How it connects

### Square: clients, invoices and money

- **Clients come only from Square customers**, plus any made in the app (which are created in Square too). A name entered in Square as `Name @brand` becomes the client plus a business.
- **Revenue comes only from recorded payments**: Square payments minus refunds, plus cash income you add by hand. Square's processing fees are listed separately and only come off the net figure. What clients still owe appears separately as *expected*, with its own list where a project paid outside an invoice can be marked paid.
- **"Owes" comes from the invoice.** When a project has a Square invoice, what it owes is that invoice's balance, partial payments included. An invoice Square marks paid always counts as fully paid.
- **Invoice composer.** Pick items from the Square item library or type custom ones, then set the due date, deposit, discount, tips, payment methods, payment reminders and delivery: email, text, both, or just a link. With both, Square emails the invoice and Messages opens with the link ready to send, since Square's API sends one way per invoice. Send it or save it as a draft. A new invoice also creates its project, with the project's own due date, status, brief and notes filled in right there.
- Invoices created in Square itself after setup also become projects automatically.
- Re-syncing is idempotent: payments, invoices and clients are matched by their Square IDs, so nothing is duplicated.

The access token is stored in the iOS Keychain.

### Calendar

- **Due dates on your calendar.** Each active project's due date is an all-day event on the calendar you pick (any calendar on the phone, including Google or Outlook ones added in iOS Settings). It moves when the date changes and is removed when the project is finished or deleted.
- **Today's events** from the calendars you choose appear on Today. Atelier's own due-date events are left out there, so each deadline shows once.

### Mail

A small IMAP and SMTP client written for the app, with presets for Gmail and iCloud and manual settings for any other host, and support for several accounts. Swiping a message archives it to the server's Archive folder, creating one if needed. Delete moves a message to Trash, and deleting it from Trash removes it for good.

- **Signatures** per account, plus **templates and saved replies** with `{first}`, `{name}` and `{business}` filled in.
- **Attachments:** open them with Quick Look, and attach photos or files when writing. Forwarding keeps them.
- **Drafts** save to the server's Drafts folder when you cancel a message.
- **Star** (the IMAP flag, so it shows in other mail apps), **pin to top**, and **snooze** (hidden, then back with a notification).
- **Replied** messages are marked on the server and show a reply arrow.
- **Clients:** a message from a client's or business's address shows that client; other senders get "Link to client" with suggestions. A message can be linked to a project, and each client's page lists your conversations.
- **Select several** messages to mark read or unread, star, archive or delete them. Search also matches attachment names in mail you've opened.

## Organizing

- **Favorite projects and pinned clients** sort to the top.
- **Select several** projects or clients for bulk actions: complete, set status, mark paid, favorite, archive, pin or remove.
- **Recently viewed** records show in Search before you type.
- **Quick Capture:** press and hold the tab bar from anywhere to add a project, client, invoice, email, expense or income.
- **Monthly summary:** income, processor fees, expenses, projects started and completed, new clients and top clients, with a notification on the 1st.
- Context menus on projects, clients, invoices, transactions and mail, and a loading skeleton for mail.

## Your data

- **Automatic backups** run daily, every three days or weekly when you leave the app, and keep the last 7 to 60. They're plain files in the Files app (On My iPhone → Atelier → Backups), so they don't depend on any sync service.
- **A second copy** of every backup can go to any folder you pick in Files: iCloud Drive, a USB drive, another app. If that folder can't be reached (iCloud signed out, folder moved), the backup still saves on the phone and Settings says why.
- **Export everything** to one file: all records plus settings, the Today layout, mail templates and the logo. Mail passwords and the Square token are never included.
- **Import with a preview.** Before anything is added, Atelier shows what's new and what's already there. Duplicates are found by id and by content (the same client, the same project on the same day, the same payment), and existing records always win, so an import can't undo later changes. A backup of the current data is saved first.
- **Sync & Backups** shows each connection's last good sync and any error, with a retry button; Today shows a one-line warning when something stops syncing.
- **Updates can't cost data:** before a new version opens the database, a copy of it is put aside, and the database opens through a versioned schema with a migration plan for future changes.
- **Nothing important disappears without a way back:** deletes go to Recently Deleted, erasing everything saves a backup first, and deleting for good (from Recently Deleted or a mail Trash folder) always asks.

## Safety net

- **Recently Deleted** (Settings → Sync & Backups) keeps deleted projects, clients and transactions for 7 days to a year (30 by default). Restoring brings back their links: a client's businesses and projects, and a project's calendar event.
- **Shake to undo** the last edit, completion or delete, after a confirmation. Sync changes stay off the undo list.
- **Automatic saving:** swipe away an edited project or client and the change is kept; Cancel throws it away. Unsent mail is offered as a draft.
- **Haptic confirmations** when you complete a project, mark it paid, save, or send an invoice or email.

## Settings

- **Business profile:** logo, name, email, phone, website and address.
- **Currency:** the most used currencies, each with its symbol.
- **Formats:** date style (Oct 31, 31 Oct, 10/31, 31/10), 12- or 24-hour time, and the first day of the week, used everywhere from Finance to the calendar.
- **Defaults:** status and due date for new projects (new projects start as Not Started); due date, deposit, tips and payment terms for new invoices.
- **Notifications:** deadline reminders (day of, day before, two days before), an overdue nudge, a morning summary, a monthly summary, invoice paid or overdue, and new mail, grouped by kind.
- **Privacy & Lock:** Face ID, Touch ID or passcode lock with a delay, behind a blur with a single Unlock button that fades away; an optional blur for the app switcher that fades in as you swipe away; and amounts in widgets hidden while the iPhone is locked.
- **App icon:** Black (the default), White, and a glass version of each.
- **What's New:** the changelog, inside Settings.

## Widget

One configurable "Atelier" widget in small, medium and large sizes, which shows one of the following:

- due today
- upcoming
- income
- calendar
- invoices
- quick add
- mail

The large Calendar is a month grid with dots for events and deadlines. Tapping a day shows that day's events, and the widget goes back to today after 30 seconds. Lock Screen widgets show what's due or this month's income.

With "Hide amounts in widgets" on, amounts are marked private, so iOS hides them on the Lock Screen and in Today View while the iPhone is locked, and shows them on the Home Screen.

The app writes a small snapshot to its App Group and the widget reads it, so the widget never opens the database.

## Under the hood

- **SwiftUI and SwiftData** on iOS 26, built with Xcode 27.
- **WidgetKit with App Intents** for the configurable widget and the tappable calendar days.
- **EventKit** for due-date events and today's schedule, **BackgroundTasks** for refreshes, and local notifications for deadlines, overdue work, paid invoices, a daily summary and new mail.
- **Square's REST API** for customers, catalog, orders, invoices and payments. It's the only web service the app talks to.
- **Hand-written IMAP, SMTP and MIME** (quoted-printable, base64, encoded headers, IMAP's UTF-7 folder names) on top of `URLSessionStreamTask`, including STARTTLS.
- **A privacy shield** in its own window above the app, so the app-switcher blur and the lock cover open sheets too.
- **JSON export, import and file backups**, plus CSV import for Square transaction exports and bank statements.

All data stays on the phone, apart from what syncs with the user's own Square and mail accounts and the due dates written to their calendar. There's no Atelier server and no analytics.

## Design

Black background, white type and monochrome glass by default, from the floating tab bar to the cards, sheets and widget. Color appears only where it carries meaning, such as overdue dates and calendar colors.

- **Appearance:** Dark (the original), Light, or follow the system, switching live, even with Settings open. Every screen is drawn from a few adaptive colors (ink, paper, accent), so both modes stay consistent.
- **Accent:** Monochrome or one of seven colors, used for selected tabs and chips, main buttons and switches.
- **One set of controls:** choices like Day/Week/Month/Year, Dark/Light/System, Income/Expense and mail providers all use the same chips.
- **Accessibility:** large figures grow with your text size, rows read as one item in VoiceOver with favorite, pinned, starred and unread states announced, and loading animations respect Reduce Motion.

## How it's tested

Atelier has a built-in end-to-end self-test, over 130 checks, run in the Simulator. It covers:

- client matching and de-duplication
- finance totals, with processor fees kept apart from expenses
- decoding Square JSON (shapes copied from real responses)
- invoice → project creation
- MIME
- backup round-trips
- search ranking
- attaching projects to clients by hand
- keeping the sample workspace away from real data and services
- due dates written to, moved on and removed from a calendar
- the Today layout: old layouts carrying over, presets, pairing small widgets, moving and resizing
- export and import: settings and records in the file, duplicates found by content, previews that change nothing
- backup files, retention, sync status and opening the database through the migration plan

Mail (sending, attachments, archiving, drafts, flags and delete) runs against a small fake IMAP/SMTP server written in Python. An optional live Square check is read-only and verifies that re-syncing never duplicates anything.

Sample data (from Settings, or a launch flag for screenshots) opens a separate in-memory workspace that stands in for everything, mail included. While it's open nothing syncs with Square or the calendar, the widget keeps showing real data, and exiting brings the real workspace back untouched.

## Status

In daily use on one iPhone. There are no builds to download.

© 2026 Byaydenrx. All rights reserved.
