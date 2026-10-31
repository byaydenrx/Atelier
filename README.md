# Atelier

A personal studio app for iPhone, built for one freelance designer's commission business. Atelier keeps projects, clients, Square invoices, money, mail and notes in one place. It stays in sync with the tools the work already lives in: a Reminders list, Square, an IMAP mailbox and Calendar.

SwiftUI and SwiftData, with a home-screen widget, in a black, monochrome Liquid Glass design.

> **About this repository.** Atelier is a private app, made for one person's workflow, and its source code isn't published. This repository documents what it does, how it's put together and the decisions behind it. There's nothing here to build or download.

## Why it exists

Commission work was spread over four apps. Who ordered what lived in Reminders, payments in Square, conversations in email and pricing notes in Notes. Answering "who still owes me?" meant cross-checking all of them.

Atelier doesn't replace those apps. It reads and writes them, so each one keeps working on its own and the iPhone has one view across all of them.

## What's in it

Today · Projects · Clients · Invoices · Finance · Mail · Notes, with Search on the side. You can reorder or hide tabs and the sections on Today.

| Tab | What it shows |
| --- | --- |
| **Today** | What's due and overdue, active projects with progress and what's still owed, upcoming calendar events, pinned notes |
| **Projects** | Every commission with its client, brand, price, what's owed, status (Not Started, In Progress, Waiting, Completed) and its invoice's status |
| **Clients** | Square customers, their brands and Instagram handles, active and past projects, total owed. Brands are added and edited right in the client form, websites open with one tap, and any project can be attached to a client by hand |
| **Invoices** | Square invoices with status and balance; write a new one without leaving the app |
| **Finance** | Income, expenses and fees by day, week, month or year, with history and what's still expected. Tap a bar in the chart to see that day's income and expenses |
| **Mail** | One or more IMAP/SMTP accounts: read, reply, compose, archive |
| **Notes** | Work notes, synced through a mail account's Notes folder |
| **Search** | One box across everything, ranked so names that start with what you typed come first |

## How it connects

### Reminders: the commission list

Every reminder in one chosen list is one project, and every project is one reminder. Edits go both ways.

Reminders are written the way they'd be typed by hand:

```
Title:  Maya Chen @lumenrecords
Notes:  $400 / Album cover
        owes $200
Due:    Nov 5
```

- The title is the client, optionally followed by `@brand`. Extra words, counts like `2/3` and notes in brackets are understood.
- The notes hold the work and the price in either order (`$120 / Longsleeve` or `2 Pcs / $250`), with `owes $…` on its own line or the same line. "Fully paid" means nothing is owed.
- Only the date of the due date matters; times are ignored.

When the app writes back, it keeps the existing wording and changes only what changed: the amount owed, the due date or the done state. New projects created in the app become new reminders in the same format, which also puts them on the calendar.

### Square: clients, invoices and money

- **Clients come only from Square customers.** Reminders never create clients; a reminder links to a client when its title names one. If the Square customer shows up later, the project links on the next sync. A project whose reminder doesn't name its client can be attached by hand; the app remembers that spelling so the link survives later syncs. A name entered in Square as `Name @brand` becomes the client plus a brand.
- **Revenue comes only from Square payments**, minus refunds. Square's processing fees become expenses. Nothing from Reminders is counted as income, so nothing is counted twice. What clients still owe appears separately as *expected*.
- **"Owes" comes from the invoice.** When a project has a Square invoice, what it owes is that invoice's balance, partial payments included. Projects without an invoice use the amount in their reminder.
- **Invoice composer.** Pick items from the Square item library or type custom ones, then set the due date, deposit, discount, tips, payment methods, reminders and delivery: email, text, both, or just a link. With both, Square emails the invoice and Messages opens with the link ready to send, since Square's API sends one way per invoice. Send it or save it as a draft. A new invoice can also create its project and reminder in one step, with the project's own due date, status, priority, type, brief and notes filled in right there.
- Invoices created in Square itself after setup also become projects automatically.
- Re-syncing is idempotent: payments, invoices and clients are matched by their Square IDs, so nothing is duplicated.

The access token is stored in the iOS Keychain.

### Mail

A small IMAP and SMTP client written for the app, with presets for common hosts and support for several accounts. Swiping a message archives it to the server's Archive folder, creating one if needed. Nothing is deleted from the app.

### Notes

Apple has no API for iCloud Notes. Instead, Atelier syncs a folder of notes that Apple Notes keeps in a mail account (the "Notes" setting under that account on iPhone). Each note is a message in that folder, so edits on either side show up on the other.

### Calendar

Read-only. Reminders with due dates already appear in Calendar, so Atelier adds no events of its own and each project shows up once.

## Organizing

- **Tags with colors** on projects, filter Projects by tag, and manage them in Settings → Tags.
- **Favorite projects and pinned clients** sort to the top.
- **Select several** projects or clients for bulk actions: complete, set status, mark paid, tag, favorite, archive, pin or remove.
- **Recently viewed** records show in Search before you type.
- **Saved invoice items** of your own, next to the Square item library; save any line from the composer with a swipe.
- **Quick Capture:** press and hold the tab bar from anywhere to add a project, client, invoice, note, email, expense or income.
- **Monthly summary:** income, expenses, projects started and completed, new clients and top clients, with a notification on the 1st.
- Context menus on invoices and transactions, and a loading skeleton for mail.

## Settings

- **Business profile:** logo, name, email, phone, website, address and opening hours.
- **Formats:** date style (Oct 31, 31 Oct, 10/31, 31/10), 12- or 24-hour time, and the first day of the week, used everywhere from Finance to the calendar.
- **Defaults:** status, price and due date for new projects; due date, deposit, tips and payment terms for new invoices.
- **Notifications:** quiet hours (scheduled reminders move to when they end; mail and payment alerts arrive silently), quiet outside business hours, and notifications grouped by kind.
- **Privacy & Lock:** Face ID, Touch ID or passcode lock with a delay; amounts hidden until Face ID; a blurred app switcher; amounts hidden on widgets.
- **App icon:** Black Glass, White, Graphite or Outline.
- **What's New:** the changelog, inside Settings.

## Widget

One configurable "Atelier" widget in small, medium and large sizes, which shows one of the following:

- due today
- upcoming
- income
- calendar
- invoices
- quick add
- notes
- mail

The large Calendar is a month grid with dots for events and deadlines. Tapping a day shows that day's events, and the widget goes back to today after 30 seconds. Lock Screen widgets show what's due or this month's income.

The app writes a small snapshot to its App Group and the widget reads it, so the widget never opens the database.

## Under the hood

- **SwiftUI and SwiftData** on iOS 26, built with Xcode 27.
- **WidgetKit with App Intents** for the configurable widget and the tappable calendar days.
- **EventKit** for Reminders and Calendar, **BackgroundTasks** for refreshes, and local notifications for deadlines, overdue work, paid invoices, a daily summary and new mail.
- **Square's REST API** for customers, catalog, orders, invoices and payments. It's the only web service the app talks to.
- **Hand-written IMAP, SMTP and MIME** (quoted-printable, base64, encoded headers, IMAP's UTF-7 folder names) on top of `URLSessionStreamTask`, including STARTTLS.
- **A parser for Reminders entries**, versioned, so it can re-read old reminders when the rules improve.
- **JSON backup and restore**, plus CSV import for Square transaction exports and bank statements.

All data stays on the phone, apart from what syncs with the user's own Reminders, Square and mail accounts. There's no Atelier server and no analytics.

## Design

Black background, white type and monochrome glass, from the floating tab bar to the cards, sheets and widget. Color appears only where it carries meaning, such as overdue dates and calendar colors.

## How it's tested

Atelier has a built-in end-to-end self-test, nearly 120 checks, run in the Simulator. It covers:

- the Reminders parser and write-back against real-world entry formats
- client matching and de-duplication
- finance totals
- decoding Square JSON (shapes copied from real responses)
- invoice → project → reminder creation
- MIME
- backup round-trips
- search ranking
- attaching projects to clients by hand
- keeping the sample workspace away from real data and services
- Reminders and Calendar sync against a throwaway list

Mail, archiving and notes sync run against a small fake IMAP/SMTP server written in Python. An optional live Square check is read-only and verifies that re-syncing never duplicates anything.

Sample data (from Settings, or a launch flag for screenshots) opens a separate in-memory workspace that stands in for everything, mail included. While it's open nothing syncs with Square, Reminders or Notes, the widget keeps showing real data, and exiting brings the real workspace back untouched.

## Status

In daily use on one iPhone. It's a personal tool, not a product, so there are no builds to download and no plans for the App Store.

© 2026 Byaydenrx. All rights reserved.
