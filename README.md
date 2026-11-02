# Atelier

A personal studio app for iPhone, built for one freelance designer's commission business. Atelier keeps projects, clients, Square invoices, money and mail in one place, and puts project due dates on the calendar.

SwiftUI and SwiftData, with a home-screen widget, in a black, monochrome Liquid Glass design.

> **About this repository.** Atelier is a private app, made for one person's workflow, and its source code isn't published. This repository documents what it does, how it's put together and the decisions behind it. There's nothing here to build or download.

## Why it exists

Commission work was spread over several apps: payments in Square, conversations in email, due dates on a list. Answering "who still owes me?" meant cross-checking all of them.

Atelier brings that together. Square stays the source of truth for clients and money, mail stays on the mail server, and due dates go to the calendar you already look at.

## What's in it

Dashboard · Projects · Clients · Invoices · Finance · Mail, with Search on the side. You can reorder or hide tabs and the widgets on the Dashboard. Hold the tab bar and slide your finger to move between tabs (the selection flows along like a drop of liquid, and the icons under it change colour), or swipe sideways on any empty space. Every row lights up the moment you tap it, then the page opens, so you see what you picked.

| Tab | What it shows |
| --- | --- |
| **Dashboard** | Widgets you arrange yourself (see below) |
| **Projects** | Every commission with its client, business, price, what's owed, status (Not Started, In Progress, Completed, Cancelled, or your own) and its invoice's status, as a list or a calendar |
| **Clients** | A small CRM: each client's businesses, contact details, projects, money and history (see below). **Current**, **Recents**, **Top** and **All** tabs, each with a count |
| **Invoices** | Square invoices with status and balance; write a new one without leaving the app, with its project set up the same way as New Project and the next invoice number shown |
| **Finance** | Income, expenses and profit by day, week, month, year or a custom range, plus analysis pages (see below). Processor fees are kept apart from expenses, in their own box under the Expenses tab. A search bar finds any transaction by name, client, project or amount |
| **Mail** | One or more IMAP/SMTP accounts: read, reply, compose, archive, delete |
| **Search** | One box across everything, ranked so names that start with what you typed come first |

## Dashboard

The Dashboard is a grid of widgets, each small (half width) or wide. Hold any empty space, or hold a widget and tap **Edit Dashboard**: the widgets jiggle like the Home Screen, and you can drag them into a new order, resize them, remove them, or add more from a gallery. Tap empty space or Done to finish. Presets fill the Dashboard in one tap: At a Glance, Project Focus, Money Focus, Weekly Review and Minimal.

The widgets:

- **Essentials:** income overview with quick actions, quick-create buttons, a daily summary (due, overdue, money in today, next event, unread mail).
- **Projects:** due today, overdue, needs attention, upcoming deadlines, awaiting payment, recently updated, active project cards, and a workload chart by status.
- **Money:** income today, this week and this month; outstanding invoices; expected income; a monthly goal with progress; this week against last week; a business health check (income pace, overdue work and invoices, what's due); recent transactions and recent expenses.
- **Schedule and mail:** a month calendar of due dates, upcoming events, unread mail.

The header can show a time-of-day greeting, your own greeting, or none, and the date in full, short, or not at all. **Screen privacy** hides every amount in the app, for showing your screen to someone or working in public.

## Clients

Each client has one profile with the details that matter once: full name, email, phone, Instagram, billing address (with address suggestions as you type), notes, pricing notes (negotiated rates, discounts, special arrangements) and custom fields of your own. Businesses are the one thing a client can have several of, each with its own email, Instagram, phone and website.

- **Money at a glance:** average project, what's still owed and the number of projects, then a **lifetime value** chart: the total, and the work booked month by month.
- **Work:** active, completed, archived and cancelled projects (with the reason) and invoices.
- **Activity timeline:** projects started and finished, status changes, payments, invoices, emails sent and received, and notes, calls, meetings and messages you log.
- **Last contacted** updates on its own when you email a client or a client emails you.
- **Merge duplicates:** projects, invoices, payments, businesses and notes move to the client you keep. A merged Square customer keeps landing on the right client.
- **Recents** lists clients added, or with a new project or invoice, in the last 30 days. **Top** shows the best clients by what they've paid, repeat clients and how much of the revenue they bring, and new and returning clients this year.
- **Filters** for money: who owes money or is all paid, anything overdue, no payments yet, and paid, owed or average project above an amount. The matching figure shows beside each name. Sort by name, revenue, amount owed, average project or newest.

## Projects

- **Dates:** a start date and due date on every project. Days overdue are counted for you. A **calendar view** shows starts and due dates by month.
- **Statuses of your own** ("Sketching", "At the printer"), each sitting in a built-in stage, and the **time spent in each status**.
- **History:** status changes, payments, moved deadlines and important edits, newest first.
- **Money:** record payments and deposits as they come in. They go into Finance tied to the project and client and come off what's owed. Add an expense by picking one already in Finance (from Square or added by hand) or a new one; profit is worked out after the project's own expenses.
- **Billing:** a fixed price, hourly, or a retainer. Hourly projects have a **timer** (one runs at a time) and time added by hand; unbilled hours go onto a Square invoice as one line, or onto what's owed. Rates come from the project, the client or a default. A retainer adds its amount to what's owed every week, month, quarter or year, catching up once for each missed date.
- **Templates:** save a project's price, status, timing and brief and start new ones from it. Projects can also be **duplicated for another client**, **pinned**, **archived**, **cancelled with a reason**, and **edited in bulk** (dates, client, status).
- **Notes** right on the project page.

## Finance

- **Income and payments:** income received, expected income and money owed, partial payments and deposits, and recurring income. Payments can be in **another currency**: the amount as paid is kept, and it's converted at that day's European Central Bank rate (fetched only when you ask) so totals add up.
- **Expenses:** one tap away under the Expenses tab, with Square's processor fees and recurring costs in their own boxes beside them.
- **Expected:** aging in 0–30, 31–60, 61–90 and 90+ days, and a forecast built only from agreed money (open invoices and project balances) by due date.
- **Reports:** revenue over the last 12 months with profit, and month-by-month and year-over-year comparisons. Tap any chart or figure to see the transactions behind it.
- **Business overview and health:** a 0–100 score from the revenue trend, how old unpaid money is and deadlines kept, with this month against last month and the same month a year ago, the current workload, and averages (project value, client value, time to finish a project).
- **Tax estimate** to set aside on income minus expenses and fees, using built-in 2026 rates for the US (federal, self-employment and state), the UK, Canada and Australia, or a flat rate. It's a guide, not tax advice.
- **Export:** transactions as CSV (date, type, title, amount, client, project, source, fee, notes), and PDF reports for any range, including a monthly business report.

## How it connects

### Square: clients, invoices and money

- **With Square connected, clients come only from Square customers**, plus any made in the app (which are created in Square too). Without Square, clients and payments are added by hand. A name entered in Square as `Name @brand` becomes the client plus a business.
- **Revenue comes only from recorded payments**: Square payments minus refunds, plus payments you record by hand. Square payments are tied to their client and project automatically. Square's processing fees are listed separately and only come off profit. What clients still owe appears separately as *expected*.
- **"Owes" comes from the invoice.** When a project has a Square invoice, what it owes is that invoice's balance, partial payments included. An invoice Square marks paid always counts as fully paid.
- **Invoice composer.** Pick items from the Square item library or type custom ones, then set the due date, deposit, discount, tips, payment methods, payment reminders and delivery: email, text, both, or just a link. With both, Square emails the invoice and Messages opens with the link ready to send, since Square's API sends one way per invoice. Send it or save it as a draft. The invoice's title is also its new project's, with the brief and private notes in the same section and the project's own due date and status below.
- Invoices created in Square itself after setup also become projects automatically.
- Re-syncing is idempotent: payments, invoices and clients are matched by their Square IDs, so nothing is duplicated.

**Connecting:** sign in with Square in a pop-up browser (Square's own page, so the app never sees the password), or paste an access token. Either way the token is kept in the iOS Keychain and only sent to Square. Sign-in renews itself before the token expires. On the first-launch welcome, "How do you get paid?" offers Square or Manual; with Square, Continue opens the sign-in and moves on once you're connected.

### Invoices without Square

Without Square, Atelier makes the invoice itself: a PDF with your business details and how clients pay you, emailed from your own mail account or shared. Mark it paid when the money arrives, and its project's balance follows.

### Calendar

- **Due dates on your calendar.** Each active project's due date is an all-day event on the calendar you pick (any calendar on the phone, including Google or Outlook ones added in iOS Settings). It moves when the date changes and is removed when the project is finished or deleted.
- **Today's events** from the calendars you choose appear on the Dashboard. Atelier's own due-date events are left out there, so each deadline shows once.

### Coming later: PayPal, Stripe and bank accounts

PayPal and Stripe payments, PayPal and Stripe invoices, and bank accounts (SimpleFIN or statement files) are built and tested, with matching that counts each payment once across all of them. They're hidden for now, until each has a sign-in anyone can use. For now Atelier works with Square, or by hand.

### Mail

A small IMAP and SMTP client written for the app, with presets for Gmail, iCloud and Outlook and manual settings for any other host, and support for several accounts. Gmail and iCloud use an app password, with the steps and a link to the right page shown in the app. Outlook, Hotmail and Microsoft 365 sign in with Microsoft (XOAUTH2), since Microsoft no longer allows passwords for mail apps; that needs Atelier's Microsoft app registration, which isn't set up yet. Swiping a message archives it to the server's Archive folder, creating one if needed. Delete moves a message to Trash, and deleting it from Trash removes it for good.

- **Signatures** per account, plus **templates and saved replies** with `{first}`, `{name}` and `{business}` filled in.
- **Designed emails** (receipts, form submissions, newsletters) show as their sender made them, on a white card fitted to the phone, and the whole message scrolls as one page.
- **Pictures** show inside the message, the way the other person sees them. Photos you attach go inside the email you send, under your text, not just as files.
- **Attachments:** open them with Quick Look, and attach files when writing. Forwarding keeps them.
- **Drafts** save to the server's Drafts folder when you cancel a message.
- **Star** (the IMAP flag, so it shows in other mail apps), **pin to top**, and **snooze** (hidden, then back with a notification).
- **Replied** messages are marked on the server and show a reply arrow.
- **Clients:** a message from a client's or business's address shows that client; other senders get "Link to client" with suggestions. A message can be linked to a project, and each client's page lists your conversations.
- **Select several** messages to mark read or unread, star, archive or delete them. Search also matches attachment names in mail you've opened.

## Organizing

- **Pinned projects and clients** sort to the top.
- **Select several** projects or clients for bulk actions: edit dates, client or status, complete, mark paid, pin, duplicate, archive or remove.
- **Recently viewed** records show in Search before you type.
- **Quick Capture:** the + button adds a project, client, invoice, email, expense or income.
- **Shortcuts and Siri:** new project, new client, log an expense (with the amount and what it was), start a timer, "what's due today" and "income this month" (answered without opening the app).
- **Save to Atelier** from the share sheet: text or a link from Mail, Messages, Instagram or Safari becomes a new project or client the next time the app opens.
- **Monthly summary:** income, processor fees (in their own box), expenses, projects started and completed, new clients and top clients, with a notification on the 1st.
- Context menus on projects, clients, invoices, transactions and mail, and a loading skeleton for mail.

## Your data

- **Automatic backups** run daily, every three days or weekly when you leave the app, and keep the last 7 to 60. They're plain files in the Files app (On My iPhone → Atelier → Backups), so they don't depend on any sync service.
- **A second copy** of every backup can go to any folder you pick in Files: iCloud Drive, a USB drive, another app. If that folder can't be reached (iCloud signed out, folder moved), the backup still saves on the phone and Settings says why.
- **Export everything** to one file: all records plus settings, the Dashboard layout, mail templates and the logo. Mail passwords and the Square token are never included.
- **Import with a preview.** Before anything is added, Atelier shows what's new and what's already there. Duplicates are found by id and by content (the same client, the same project on the same day, the same payment), and existing records always win, so an import can't undo later changes. A backup of the current data is saved first.
- **Sync & Backups** shows each connection's last good sync and any error, with a retry button; the Dashboard shows a one-line warning when something stops syncing.
- **Updates can't cost data:** before a new version opens the database, a copy of it is put aside, and the database opens through a versioned schema with a migration plan for future changes.
- **Nothing important disappears without a way back:** deletes go to Recently Deleted, erasing everything saves a backup first, and deleting for good (from Recently Deleted or a mail Trash folder) always asks.

## Safety net

- **Recently Deleted** (Settings → Sync & Backups) keeps deleted projects, clients and transactions for 7 days to a year (30 by default). Restoring brings back their links: a client's businesses and projects, and a project's calendar event.
- **Undo:** deleting a project, client or transaction, or archiving or deleting an email, shows a small pill with **Undo**. Shaking the iPhone undoes the same thing, or the last edit or completion, after a confirmation. Archived and deleted emails are found again by their Message-ID and moved back. Sync changes stay off the undo list.
- **Automatic saving:** swipe away an edited project or client and the change is kept; Cancel throws it away. Unsent mail is offered as a draft.
- **Haptic confirmations** when you complete a project, mark it paid, save, or send an invoice or email.

## Feedback

**Make Atelier Better**, a page at the bottom of Settings, collects ideas and bug reports, and the roadmap is built from them. All of it lives in this repository's [Issues](https://github.com/byaydenrx/Atelier/issues).

- **Sending:** pick Feature Request, Bug Report or Other, write it, attach up to four screenshots and tap Submit Feedback. Each submission becomes an issue labelled with its category. Words are kept until they're sent, so leaving Settings never loses them.
- **With or without a GitHub account:** with a GitHub token connected (on the same page, kept in the Keychain), feedback is posted from the app. Without one, GitHub's new-issue page opens already filled in, with screenshots copied for pasting.
- **Screenshots** are shrunk and committed to a separate `feedback-assets` branch, so the main branch stays documentation only. The form warns that feedback is public, so screenshots should be checked for client names and amounts.
- **Community Roadmap:** what's In Development, and the Most Requested features ranked by votes. Votes are 👍 reactions on the issue: from the app when GitHub is connected, otherwise on github.com. The list is cached, so it opens offline.
- **Feedback Inbox:** only shown when the connected token can manage the repository. It filters by New, Planned, In Development or Closed, by category and by search, and sorts by date or votes. Swipe right to plan or start a request, left to finish or decline it. Each request shows its screenshots and comments, and you can change its status or category and reply. Statuses are labels; Done and Won't Do close the issue as completed or not planned.

## Price and license

Atelier is a one-time purchase: **$19.99**, no subscription. It starts with a **14-day free trial** with every feature open, and nothing interrupts the trial: no pop-ups or reminders. The top of Settings shows how many days are left, then **Purchase a License**, **Activate Your License** and **Restore Purchases**.

- Licenses are sold outside the App Store and arrive as a key by email. Atelier keys are signed and checked on the device, with no account and no server; keys from an online store can also be activated over the internet.
- A license is saved in the iCloud Keychain, so **Restore Purchases** picks it up on the user's other iPhones, iPads and Macs, and it survives reinstalling.
- When the trial ends, everything already in the app stays there to look through and export; adding and editing wait for a license.
- The developer's own build always has full access.

Licenses aren't on sale yet.

## Settings

- **Business profile:** logo, name, email, phone, website and address.
- **Currency:** the most used currencies, each with its symbol.
- **Formats:** date style (Oct 31, 31 Oct, 10/31, 31/10), 12- or 24-hour time, and the first day of the week, used everywhere from Finance to the calendar.
- **About Atelier:** version, support, the privacy policy, terms and acknowledgements.
- **First launch:** a short welcome that lists what's in the app, asks your name and business, connects Square (or lets you work by hand) and explains the trial.
- **Project statuses and templates.**
- **Defaults:** status and due date for new projects (new projects start as Not Started); due date, deposit, tips and payment terms for new invoices.
- **Notifications:** deadline reminders (day of, day before, two days before), an overdue nudge, a morning summary, a monthly summary, invoice paid or overdue, and new mail, grouped by kind.
- **Privacy & Lock:** Face ID, Touch ID or passcode lock with a delay, behind a blur with a single Unlock button that fades away; an optional blur for the app switcher that fades in as you swipe away (otherwise the switcher shows the app as it is); and amounts in widgets hidden while the iPhone is locked.
- **App icon:** Black (the default), White, and a glass version of each.
- **What's New:** the changelog, next to Make Atelier Better at the bottom of Settings.

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
- **Square's REST API** for customers, catalog, orders, invoices and payments, with OAuth (PKCE) sign-in, and, once they're switched on, **PayPal's** and **Stripe's** APIs and **SimpleFIN** for bank accounts. Besides those, the app only talks to GitHub (for feedback), Apple Maps (address suggestions), the European Central Bank's rates through frankfurter.dev (when you ask for a rate) and, when a store-bought key is activated, the store's license check.
- **App Intents** for Shortcuts and Siri, and a **share extension** that hands items to the app through the App Group.
- **iPhone and iPad**, with the iPad (and Mac) layout in a centered column; a **Mac Catalyst** build runs locally.
- **os.Logger** with private fields marked, so logs never show client names or amounts.
- **CryptoKit** (Ed25519) to check license keys on the device, and the iCloud Keychain to carry them to the user's other devices.
- **PDF reports** drawn with UIKit's PDF renderer, and Swift Charts for every chart.
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

Atelier has a built-in end-to-end self-test, 261 checks, run in the Simulator, plus a Swift Testing target for the core logic (`xcodebuild test`) and a speed test that times the heavy work on five years of a busy studio (1,000 clients, 3,000 projects, 10,000 payments). It covers:

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
- the Dashboard layout: old layouts carrying over, presets, pairing small widgets, moving and resizing
- export and import: settings and records in the file, duplicates found by content, previews that change nothing
- backup files, retention, sync status and opening the database through the migration plan
- feedback: issue text and titles, screenshot handling, the github.com fallback, the roadmap's order, votes, statuses and replies
- undo: deletes coming back with their links, staying off the edit undo list, and archived or deleted mail returning to the inbox
- clients: custom fields, money totals, money filters and the figure shown beside each name, the activity timeline, last contacted and merging duplicates
- projects: recorded payments and deposits, profit, custom statuses, time in status, templates and duplicates
- Square sign-in: the PKCE challenge, the sign-in link and checking Square's reply
- mail: pictures sent inside the message and shown where the sender put them, and the Outlook sign-in strings
- time tracking, billing hours, retainers, and PayPal payments (against a fake PayPal API)
- money from anywhere: bank statements (CSV, OFX), SimpleFIN and Stripe against fake servers, and the matching that keeps payouts, transfers, card payments and payments already recorded from being counted twice
- invoices without Square: who sends them, Atelier's PDF invoices paid from the bank, PayPal and Stripe invoices against fake APIs (nothing is ever emailed), and Stripe sign-in through a local copy of the sign-in helper
- finance: recurring transactions, totals, aging, the forecast, unusual expenses, the health score, tax estimates, CSV and PDF export and custom ranges
- licenses: signed keys accepted, altered or foreign keys refused, and online activation against a fake store

Mail (sending, attachments, archiving, drafts, flags and delete) runs against a small fake IMAP/SMTP server written in Python, feedback against a small fake GitHub API, license activation against a fake store, and PayPal, Stripe and bank feeds against fake APIs, so tests never post real issues or touch real money.

A second copy of the app, **Atelier 2**, is installed next to the real one for testing. It's a separate app with no access to the real data, and it starts like a fresh install every time it's opened, so the first-launch welcome, the trial and an empty workspace can be tried again and again. Its Settings can end the trial, jump to its last day or start it again, to see each stage. An optional live Square check is read-only and verifies that re-syncing never duplicates anything.

Sample data (from Settings, or a launch flag for screenshots) opens a separate in-memory workspace that stands in for everything, mail included. While it's open nothing syncs with Square or the calendar, the widget keeps showing real data, and exiting brings the real workspace back untouched.

## Status

In daily use on one iPhone. There are no builds to download yet: public builds wait on a paid Apple developer account.

© 2026 Byaydenrx. All rights reserved.
