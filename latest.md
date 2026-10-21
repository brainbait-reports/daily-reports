# Supervisor Report — 2026-10-20
- date: 2026-10-20 (America/New_York)
- video_created: queue/v0026.mp4 (vid 26)
- video_id: none
- title: A Day on Venus Is Longer Than Its Entire Year
- publish_status: failed
- qc_result: PASS (phash 26d3f215dd137fcb, 7.1MB; 1080x1920, 19.08s)
- errors_retries:
  - `publish.py --live` exited 1: upload failed at OAuth token refresh — HTTP 400
    invalid_grant, "Token has been expired or revoked." Row auto-quarantined by
    pipeline design. No retry attempted (design forbids fix-up/re-upload of a
    failed row).
  - Diagnostic (identical refresh request, credentials not echoed): creds file
    intact (client_id, client_secret, refresh_token all present); Google rejected
    the refresh token server-side. Refresh token is dead, not the file.
- duplicate_protection: vid 26 was status=queued when claimed; claimed as
  `publishing` before the upload attempt per design; only queued rows are upload
  candidates; 0 published today vs daily limit 1; no re-upload of a non-queued
  row was attempted; row is now `quarantined` with youtube_video_id empty — no
  partial or duplicate upload exists.
- api_usage: ~0 YouTube Data API units (upload never reached videos.insert; no
  videos.list verification — nothing to verify). 2 OAuth token calls (publish
  attempt + diagnostic), not quota-bearing.
- model_usage: TTS voiceover 19.1s (pipeline local TTS); 3 images via media
  pipeline (1152x2048 portrait, verified); script.txt + meta.json written by
  agent with all factual claims web-verified first; no external LLM creative.
- cost_estimate: $0 marginal
- notes:
  - First production run after Tyler lifted the 2026-10-13 stop order
    (2026-10-20 ~14:42 EDT). Kill switch confirmed publishing_enabled=true;
    daily cap check clear (0/1, America/New_York).
  - Topic #14 "A day on Venus is longer than its year" (niche=science).
    Experiment arms: script contract hook=bold_claim+caption=on; pipeline build
    ran hook=curiosity_gap+caption=off.
  - Script claims verified before writing (NASA: sidereal day ~243 Earth days,
    year ~225 Earth days, retrograde rotation so the Sun rises in the west).
  - Minor anomaly: TTS rendered the ~60-word script in 19.1s, faster than the
    25-45s contract estimated; pipeline QC still passed.
  - BLOCKER: YouTube OAuth refresh token revoked/expired (invalid_grant).
    Re-authorization requires Tyler's Google sign-in in the browser — Tobey
    cannot re-grant OAuth consent. Until re-auth, uploads will keep failing and
    each run will build then quarantine another video.
  - The 17:00 scheduled run will see 0/1 uploads and will likely attempt the
    same failing upload (same invalid_grant), quarantining another built video.
    Fix = Tyler re-authorizes YouTube OAuth; no code change needed.

## 17:00 scheduled run (same day)
- Built vid 27 "Sea Otters Hold Hands So They Don't Drift Away" (topic #13,
  niche=animals; experiment arm hook=curiosity_gap+caption=on; script + images
  web-verified; QC PASS, phash cd11322a0d6eeb7b, 7.2MB; TTS voiceover 20.9s).
- `publish.py --live` exited 1: same OAuth failure — HTTP 400 invalid_grant,
  "Token has been expired or revoked.", on the refresh-token grant. No bytes
  reached YouTube. Row 27 auto-quarantined by design. Diagnostic refresh call
  confirmed the stored refresh token itself is dead.
- duplicate_protection: 0 published today (limit 1); no upload attempt reached
  YouTube; no re-upload of quarantined row 27 attempted.
- publish_status for the 17:00 run: failed (same root cause as above).
- model_usage: 3 vertical images (1152x2048, portrait verified); TTS 20.9s.
- The 17:00 run's public report push (step 6) was skipped — pushing a
  sanitized "upload auth is broken" report is fine on credential scan, but the
  same blocker was already reported earlier today and there is no new
  publishable result; the daily report in the repo already carries this run's
  outcome via this append.
