# Test checklist (none of these have been performed yet)

Tick each item after trying it on a real phone/emulator. Run once in airplane mode.

- [ ] Project syncs and builds; APK installs; app opens without crashing
- [ ] Add employee; edit; deactivate; reactivate; delete (history still visible in Records)
- [ ] Time In (now) ; Time In again for same person is refused; Time Out; hours correct (e.g. 09:00-18:00, 60 min break = 8 h 00 m)
- [ ] Manual Time In/Out; overnight shift (22:00 → 06:00 next day) calculates 8 h minus break
- [ ] Edit a record's times → hours recalculate; delete a record; edit history shows entries
- [ ] Dashboard numbers update immediately
- [ ] Weekly, Monthly, Yearly reports (all employees and a single employee) match Records
- [ ] PDF export saves, opens, is readable and paginated; XLSX opens in Excel/Sheets with filters and numeric hour totals
- [ ] Backup export; wipe data (clear app storage); restore; everything returns; a corrupted/renamed file is rejected safely
- [ ] Close and reopen the app; reboot the phone: data remains
- [ ] Install a newer build over the old one: data remains (same signing key)
- [ ] Light/dark/system theme; 12/24-hour; date format; PIN lock/unlock; logo change
- [ ] Verify the app requests no permissions (Settings → Apps → BF Brothers Attendance → Permissions)
