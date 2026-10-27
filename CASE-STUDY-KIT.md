# Case study kit: School Management System

Everything needed to write about the project. Facts only: no clients, revenue, uptime or user counts are claimed, because none are documented.

## One-liner

An Arabic, right-to-left platform that runs a school day to day, with a separate portal where parents follow their own child.

## Descriptions

**Short.** A full-stack school management system: students and groups, attendance, progress, curriculum, subscriptions, planning and reports for the staff, and a private portal for parents. Built alone, from scratch to deployment.

**Medium.** The School Management System replaces paper and spreadsheets with one source of truth. Staff (director, supervisors, team leaders and teachers) run the school in an Arabic, right-to-left application that works on a phone, even offline for attendance. Parents sign in to a separate portal with the student's number and a 4-digit PIN and see only their own child. The business rules that must never disagree, such as who may correct a record and until when, live in the database, not in the screens.

**Long.** A school runs on many small records kept by many people. On paper and in spreadsheets they disagree, and nobody can tell who changed what. This system gives each record one home and one rule.

Staff work in one application with four primary roles (director, general supervisor, team leader and teacher) plus limited accounts for single-purpose work. Teachers take attendance with one hand on a phone: everyone starts present and only the exceptions are tapped. The dashboard points at gaps, not only totals: groups with no attendance on the last class day, students with no progress recorded this week, or a curriculum that was not updated.

Parents use a separate portal built as its own security domain, with its own sign-in, token and signing key. A parent sees one child and nothing else: attendance, progress, evaluations and medals, subscriptions and teachers' notes.

Under the interface sits a deliberately plain architecture: ASP.NET Core calls stored procedures through ADO.NET, with no ORM. Transactions, edit windows and audit rows run in the database, and the API's database login can only execute procedures.

## The problem

Records about students, attendance, progress and money are kept by many people and disagree. Staff should only see their part of the school. Leadership needs reports it can trust, and parents want to follow their child without calling the school.

## The solution

**One system, two sides.** A staff application and a family portal use the same data through two separate clients and two separate token domains.

## My role

Built alone, from scratch to deployment: design, database, API, interface and testing.

## Stack

React, TypeScript, Vite, Tailwind CSS, shadcn/ui · ASP.NET Core (.NET 10) · ADO.NET · SQL Server (stored procedures) · JWT · Playwright, Node and xUnit · GitHub Actions.

## Key numbers (counted from the source)

| | |
|---|---|
| **2** applications | The staff application and the family portal. |
| **4** primary roles | Director, general supervisor, team leader, teacher; plus limited accounts and a view-only education office account. |
| **141** API endpoints | Counted from the controllers. |
| **31** tables | Counted from the schema scripts. |
| **150+** stored procedures | Counted from the procedure scripts. |
| **55** test suites | Plus 3 C# unit-test files. The project's test README counts about 800 automatic checks. |

## Features

- **Teaching:** attendance, progress tracking, curriculum lessons and exams with grades, student evaluations and medals, weekly assignments.
- **People:** students and groups, transfers and archiving, supervision of teachers, staff accounts.
- **Finance:** monthly subscriptions, partial payments split evenly over months, financial reports.
- **Administration:** school-wide reports with PDF and Excel export, planning and notes, the audit log, scheduled automatic reports, verified backups and a health card.
- **For parents:** attendance, progress, evaluations and medals, subscriptions, teachers' notes and the weekly assignment.

## Screens

| File | Caption | Alt text |
|---|---|---|
| `01-director-dashboard.png` | The director's dashboard: notes waiting, counts and quick actions. | The director's dashboard in Arabic with counts of students, teachers, groups, supervisors, team leaders and users, and quick actions. |
| `02-groups-needing-follow-up.png` | The groups that need follow-up. | A panel listing groups marked urgent or to follow up, with tags for attendance not recorded and no progress this week. |
| `03-payment-by-month.png` | Recording a payment against months. | The payment dialog with a choice between full and partial payment, months marked paid, and a partly paid month. |
| `04-student-evaluations.png` | Student evaluations for a group. | A table of students with colored dots showing growth in nine areas on a four-step scale, and medals. |
| `05-monthly-planning.png` | Planning for the year. | Monthly cards with school, section and group plans and their status. |
| `06-members.png` | Students and staff in one list. | The members page listing students and staff with their school numbers. |
| `07-group-report.png` | An attendance report for one group. | A report for one group over a date range with attendance counts per session, with export buttons for Excel and PDF. |
| `08-groups.png` | The groups page. | A list of groups with their teachers and student counts. |
| `09-teacher-home-phone.png` | A teacher's home on a phone. | A phone screen with a reminder that last Saturday's attendance is missing and the next step. |
| `10-taking-attendance-phone.png` | Taking attendance on a phone. | A phone screen with a student list where one student is marked absent and one late, counters at the top and a save bar. |
| `11-family-sign-in-phone.png` | The family portal sign-in. | A phone sign-in with a field for the student number and a field for the 4-digit PIN. |
| `12-family-overview-phone.png` | A parent's overview of one child. | A phone screen with attendance rate, medals, remaining subscription, an attendance summary and evaluation levels. |
| `13-audit-log.png` | The audit log. | A table of actions with user, operation, date and time, such as sign-ins, attendance saved and a payment recorded. |

## Architecture summary

Controller → service → repository → ADO.NET → stored procedure. React and TypeScript on the front, an ASP.NET Core (.NET 10) API with JWT, SQL Server underneath. No ORM: rules live in stored procedures and one service layer.

## Engineering decisions

1. **Authorization beyond roles.** Two teachers can share a role without sharing students, so one access guard decides which groups and students each account can reach, checked against the data on every request.
2. **A database user that can only run procedures.** The API cannot write to tables, so it cannot skip the checks or the audit.
3. **Business rules enforced in the transaction.** Attendance is saved as one transaction (session, records, audit row). The person who recorded something can correct it for 72 hours (attendance) or 24 hours (everything else); one SQL function decides this for every record type.
4. **The family portal as a separate security domain.** Own sign-in, token audience, signing key and API client; the student always comes from the token, never from the address.

## Challenges

- Making attendance fast enough for one hand during a session, and safe to resend when the phone was offline.
- Keeping access rules identical in every screen, by putting them in one place.
- Splitting a partial payment over months so every balance can be explained.
- Protecting children's data: a parent must never reach another child, even by editing an address.

## What I learned

- Business rules shape the architecture: the question "who can correct this record, and until when?" shaped the database more than any screen did.
- Authorization is more than roles.
- Production thinking starts on day one: verified backups, health checks and clear errors matter as much as features once real people depend on a system.

## GitHub "About" description

Arabic, right-to-left school management system: attendance, progress, subscriptions, planning and reports for staff, plus a private parent portal. React, ASP.NET Core, SQL Server. Source is private; this repo shows the product and its design.

## Topics

`school-management` `education` `asp-net-core` `react` `typescript` `sql-server` `stored-procedures` `rtl` `arabic` `portfolio` `case-study` `offline-first`

## Status

Deployed and in use at a school. The source code is private; this showcase uses fictional data.
