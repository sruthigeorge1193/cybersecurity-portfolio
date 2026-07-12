
# Log Analysis Lab

## Overview
Investigated Windows and Linux system logs to detect suspicious authentication
activity and unauthorized file deletion, using the home cybersecurity lab
environment as the source system.

---

## Windows Log Analysis
Used Windows Event Viewer to review Security logs for signs of unauthorized access.

- **Failed logon attempts (Event ID 4625)** — identified a cluster of failed
  logons occurring during non-business hours, a common indicator of
  unauthorized access attempts or credential guessing.

  ![Failed login attempts](./screenshots/figure6-failed-login-attempts.png)

- **Successful logon following failures (Event ID 4624)** — a successful
  logon occurred immediately after the failed attempts, also outside
  business hours — the classic pattern of a compromised credential
  being used successfully.

  ![Successful login attempts](./screenshots/figure7-successful-login-attempts.png)

- **File deletion tracking (Event ID 4659)** — confirmed intentional deletion
  of a file via command line, cross-referenced against the Security log
  to build a verified timeline of the action.

  ![File deletion Event ID 4659](./screenshots/figure8.2-file-deletion-eventid-4659.png)

## Linux Log Analysis
Reviewed core Linux system logs to trace file deletion and user activity.

- **`/var/log/auth.log`** — authentication and session events, used to
  correlate user logon activity with file system changes.

  ![auth.log](./screenshots/figure13.1-var-log-auth-log.png)

- **`/var/log/syslog`** — system-wide event log, cross-checked against
  auth.log for a fuller picture of system activity.

  ![syslog](./screenshots/figure13.2-var-log-syslog.png)

- **Shell history (`history | grep rm`)** — used to confirm which files were
  deleted and when, directly from command history.

  ![Deleted files list](./screenshots/figure13.3-deleted-files-list.png)

## What I Learned
- How to read Windows Security Event IDs (4624, 4625, 4659) and what pattern
  of events indicates a compromised credential vs. normal activity
- How to correlate timestamps across multiple log sources (Windows Event
  Viewer, Linux auth.log, syslog, shell history) to build a single timeline
- The value of checking *both* failed and successful logons together —
  either alone tells an incomplete story

## Screenshorts

