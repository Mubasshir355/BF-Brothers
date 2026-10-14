# BF Brothers Employee Attendance (Android, fully offline)

Kotlin + Jetpack Compose + Room (SQLite). No internet, no server, no account, **no Android permissions**.

> **Status: source code only.** The APK has **not** been built and the app has **not** been compiled or run on a device or emulator.
> It was written in an environment without the Android SDK. Build it with Android Studio (see `BUILD-INSTRUCTIONS.md`),
> then run `TESTING-CHECKLIST.md` before relying on it.

## Features
- Dashboard: total employees, present today, checked in, checked out, hours today, date and live clock
- Employees: add, edit, view, activate/deactivate, safe delete (history is kept), search, per-employee history, auto IDs (BF-0001…)
- Time In / Time Out with current time or manual date-time, duplicate-open-shift prevention, overnight shifts
- Net hours = Out − In − Break; unfinished shifts show "Still Checked In" and are never counted
- Attendance Records: search, employee and date filters, add/edit/delete, edit history log
- Weekly (custom range), Monthly, Yearly reports, all employees or one employee
- Export reports to **PDF** (A4 landscape, page numbers) and real **.xlsx** (one sheet per table, header filters), saved where you choose
- Settings: light/dark/system theme, company name/address/logo, standard hours + optional overtime, default break,
  12/24-hour, date format, time zone (default Asia/Karachi), PIN lock, backup/restore, export all employees/attendance
- Backup/restore: versioned, validated JSON file

## Requirements
Android 8.0 (API 26) or newer. Permissions: none.

## Install on your phone (after you have built the APK)
1. Copy `app-release.apk` to the phone (USB, WhatsApp to yourself, Drive…).
2. Open it from the Files app and allow "Install unknown apps" for that app when asked.
3. Open **BF Brothers Attendance**.

## Daily use
1. **Add Employee** once per person. 2. **Time In / Time Out**: pick the employee, press Time In in the morning and Time Out when they leave.
3. Fix mistakes in **Attendance Records** (pencil icon). 4. **Reports** → choose Weekly/Monthly/Yearly → Export PDF or Excel.

## Protect your data
Everything is stored only on this phone. If you uninstall the app, clear its data or lose the phone, the records are gone.
Use **Settings → Export database backup** regularly (weekly is sensible) and copy the file off the phone.
Android's own cloud backup is deliberately turned off (`allowBackup=false`) so nothing leaves the device.

## Known limitations
- Logo is not included in backups (re-pick it after a restore on a new phone).
- If the time zone setting is changed later, old records keep the work-date they were saved with (exact times are stored in UTC and stay correct).
- The PIN is an access barrier, not encryption of the database.
- Reports show hours as decimals (8.50 = 8 h 30 m) so Excel can total them.
