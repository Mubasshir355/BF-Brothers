# Database and backup

Database file: `bf_attendance.db` (Room/SQLite, private app storage).

| Table | Purpose | Key columns |
|---|---|---|
| employees | people | id (auto, never reused; shown as BF-0001), name, phone, joiningDate (ISO), active, deleted |
| attendance | one row per shift | id, employeeId, workDate (ISO), timeIn (epoch ms UTC), timeOut (epoch ms or NULL), breakMinutes, remarks |
| attendance_edits | change log | attendanceId, editedAt, note |
| settings | key/value settings | settingKey, settingValue (PIN is stored as a SHA-256 hash) |

- Times are epoch milliseconds, so they stay correct if the phone's date, time zone or format changes. `workDate` is the date of Time In in the configured zone.
- "Delete employee" sets `deleted=1`: the person disappears from lists but old attendance rows and reports keep their name.
- Time Out on an open shift (even from the previous day) closes it, which supports overnight shifts. Overlapping shifts for one employee are rejected.
- Nothing is cleared on start-up; the database is never recreated by an update.

## Backup file (`BF_Attendance_Backup_YYYYMMDD_HHMM.json`)
```
{ "format": "BFAttendanceBackup", "version": 1, "createdAt": <ms>,
  "employees": [...], "attendance": [...], "edits": [...], "settings": {...} }
```
Restore checks: format name, version, every field's type, valid dates, unique ids, every attendance row pointing to an existing employee,
Time Out after Time In, break ≥ 0. Only if everything passes is the data replaced, inside one database transaction. A damaged file changes nothing.
The PIN and logo are not part of backups. Future versions must keep reading `version: 1`.
