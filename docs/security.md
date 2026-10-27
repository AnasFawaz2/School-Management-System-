# Security

## Who can see what

- **Roles are not enough.** Two teachers share a role but not students, so access is checked against the data. A teacher reaches students through their groups, a team leader through their teachers, and administrators reach everything.
- **Every request is checked on the server**, against the data and not only the menu. Typing the address of a hidden page redirects. The view-only education office has separate checks that no write path uses.
- **Every endpoint names its policy**, and access to a group or a student is verified for each request.

## The family portal is a separate domain

A parent must never reach another child's data, even by editing a URL. Families therefore have their own sign-in, token audience, signing key and API client, and the student always comes from the token. Staff and family tokens do not work on each other's endpoints.

## Accounts and sign-in protection

- **Passwords** are hashed with PBKDF2 (SHA-256). They are set by the director; nothing is e-mailed. The first account is created by a script that asks for the password and stores only the hash.
- **Staff sign-in:** after 10 wrong passwords an account and computer are blocked for 5 minutes; the next 10 for 5 minutes; the next 10 for 1 hour; then it starts over. A correct password resets the count. A computer that fails 50 times in 15 minutes is blocked for 5 minutes.
- **Family sign-in:** after 5 wrong PINs an account is locked for 15 minutes, then 1 hour, then 24 hours. The lock is kept in the database and survives restarts. A new PIN or an administrator's unlock clears it. A computer that fails 40 times in 15 minutes is blocked for 15 minutes.
- **Rate limits:** 10 sign-ins a minute per address, and 120 requests a minute per family.
- **No hints for attackers:** every failure gives the same message and does the same hashing work, so the answer does not reveal whether an account exists.
- **Session tokens** are short-lived, and the account behind each one is re-checked on every request with a short cache, so deactivating an account takes effect within seconds.

## The database

The API's database login can **only execute stored procedures** and has no rights on any table. Secrets such as the connection string and the signing key come from the server's environment, never from the code, and the API refuses to start in production without a signing key of at least 32 bytes.

## Records can't quietly change

- **Edit windows.** Whoever recorded something can correct it for 72 hours (attendance) or 24 hours (everything else). After that only administrators can.
- **Archive instead of delete.** Nothing is removed at once; it moves to an archive that only the director and general supervisors can open.
- **Audit log.** Who did what and when, for sign-ins, failed attempts, locks, attendance, payments, archiving and more. Sign-ins are kept 90 days and other actions 12 months; deleting log rows is itself recorded.

## Backups

A daily backup runs at night and is checked after it is written; the last 14 days are kept. A second, monthly backup keeps this month's and last month's file. The director's health card shows the result of the last backup. Backups should also be copied to another disk.

## In this showcase

Everything shown is a demonstration installation. All schools, teachers, parents and students are fictional.
