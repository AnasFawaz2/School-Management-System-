# How it works, role by role

All schools, people and data below are fictional (demonstration installation).

The system has two applications that share one database: the **staff application** and the **family portal**. Staff roles see more or less depending on who they are; a parent sees one child.

## Director

1. **Dashboard.** Notes waiting for the director, counts of students, teachers, groups, supervisors, team leaders and users, and quick actions (add a teacher, add a student, create a group, settings, backups, reports).
2. **Groups that need follow-up.** A list that points at gaps: no attendance recorded since the last class day, students with no progress recorded this week, or a curriculum that was not updated. Each group is marked *urgent* or *to follow up*.
3. **System health.** A card for the database, the last backup, errors today, the last automatic report and the size of the audit log.
4. **Accounts.** The director creates every other account from the *Members* page and sets the first password; nothing is e-mailed.
5. **The archive.** Deleting never removes anything at once (see below). Only the director and the general supervisors can open the archive.

## General supervisor

Runs the school day to day: students, groups, subscriptions, reports and the archive. Two **limited accounts** exist for single-purpose work: one that only sees the curriculum, and one that only sees subscriptions.

## Team leader

1. Supervises a set of teachers. A teacher may have several team leaders (shared supervision); when a team leader is created, a card picks their teachers.
2. Sees the teachers' groups and a reminder when a group's attendance is missing.
3. Writes section plans and follow-up notes for teachers.

## Teacher

1. **Takes attendance on a phone.** Everyone starts *present*. One tap on a student marks them *absent*; the menu next to a name marks *late* or *excused* (an excused absence needs a reason). *All present* resets the list.
2. **Works offline.** Without internet, the record is kept on the phone and sent by itself when the connection returns. A resend never creates a duplicate.
3. **Gets reminders.** After the class day, a teacher whose group has no attendance sees a reminder; later a second one, and the team leader is told too. They disappear once attendance is saved.
4. **Records progress and the curriculum.** Progress per student per session; lessons and exams per group, with grades for exams.
5. **Evaluates students.** Nine areas of growth on a four-step scale, and medals for steady growth.
6. **Sets the weekly assignment** for the coming class day, for one student or a whole group.

A teacher sees only their own groups. Two teachers with the same role do not see each other's students.

## View-only education office account

A read-only account for the school's education office. It can look at the dashboard, attendance, progress, curriculum, evaluations, the members directory and the reports that were shared with it, and it cannot change anything.

## Parent: the family portal

1. **Signs in** with the student's number (format `XX-XXXXX`) and a 4-digit PIN. The PIN is created by an administrator and shown once.
2. **Sees one child only:** attendance, progress, evaluations and medals, subscriptions, teachers' notes and the full history.
3. **Gets the weekly assignment** as one small alert. The parent marks it *read*, then *done*. Only that student's teachers and the administration see those steps.

## Workflows that cross roles

### Adding a student
An administrator opens *New account* on the *Members* page, chooses *student*, and fills in the student form: personal details, study, guardian and contact, and health information. The school number is filled in by itself: students and staff share one series, and numbers that were retired are never reused.

### Moving or archiving a student
A student can be transferred to another group; the move is kept in their history. Deleting a student (or a staff account, group, curriculum entry) moves it to the **archive**, with no time limit. From the archive it can be restored as it was, or deleted for good, which cannot be undone.

### Recording a subscription payment
Payments are recorded against **months**. A full payment marks the chosen months paid; a partial payment is split evenly over the months it covers, so every student's balance can be explained. The person who recorded a payment can correct it for 24 hours; after that, only administrators can.

### Monthly planning
Plans exist at three levels: the whole school, a section (a team leader and their teachers) and a single group. Each plan has a date, a category and a status: *planned*, *in progress*, *done* or *postponed*.

### Notes between staff
A note goes to one or more people. Each recipient marks it *read* or *done* and can reply.

### Reports
Attendance reports for the whole school, one group or one student, and curriculum reports, over any date range, exportable to PDF and Excel. On the first of each month the system writes the year-to-date financial, attendance and curriculum reports by itself.
