# Supervisor Report — 2026-10-22

- date: 2026-10-22 (America/New_York)
- video_created: none
- video_id: none
- title: none
- publish_status: blocked_oauth
- qc_result: not_run (no build — OAuth pre-check failed, so no tokens were burned on an unpublishable video)
- errors_retries: YouTube OAuth refresh token rejected (HTTP 400 invalid_grant: expired or revoked), reported by scripts/check_oauth.py; single pre-check call, no retries
- duplicate_protection: no publish attempted; DB shows 12 video rows, 0 with status='queued'; latest rows (20–27) all status='published'; nothing is waiting on an upload and no re-upload was attempted
- api_usage: ~0 units (one OAuth token-refresh POST only, no YouTube Data API calls)
- model_usage: none this run (no TTS, no images, no LLM creative — build was skipped per Oct 20 lesson)
- cost_estimate: $0 marginal
- notes: BrainBait channel OAuth still revoked (same state as Oct 20). Kill switch publishing_enabled=true; daily cap clear (0/1 uploads today). The lane stays ON: the next scheduled run or dependency probe re-checks and resumes automatically once Tyler reconnects the channel sign-in. Manual Studio-upload fallback remains available as an out-of-band path. Topic queue untouched.
