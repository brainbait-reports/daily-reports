# Supervisor Report — 2026-10-11
- date: 2026-10-11 (America/New_York)
- video_created: queue/v0023.mp4 (vid 23)
- video_id: 6LsCnwXj8_Y
- title: How Wombats Poop Perfect Cubes
- publish_status: published_public
- qc_result: PASS (phash 6efd6bd3eb4b607d, 9.7MB; 26.1s; 1152x2048 vertical)
- errors_retries: controller loop took 3 cycles before final exit=0:
  1) exit 10 (expected: wrote script.txt + meta.json after verifying facts
  via web search); 2) exit 11 (expected: generated 3 portrait images, all
  verified 1152x2048); 3) abort exit=1 — meta.json lacked the required
  "hook" key (the printed exit-10 contract example omitted it while the
  validator requires it); fixed by adding "hook" matching script line 1
  ("Wombats poop perfect cubes, and scientists were baffled.", 56 chars),
  then exit=0. TTS succeeded on attempt 1/3. No retries of anything
  destructive.
- duplicate_protection: row claimed as 'publishing' before upload (publish.py
  claims first); only 'queued' rows are upload candidates (vid 23 was
  'queued', confirmed in DB); 1 published today (limit 1); no re-upload of a
  non-queued row was attempted; failed rows would quarantine, none failed.
- api_usage: ~1605 units estimated (1 videos.insert ~1600 + ~5 videos.list
  ~1 each incl. post-upload verification), of 10,000 daily quota.
- model_usage: TTS voiceover 26.1s (local pipeline), 3 images via media
  pipeline (1152x2048 webp, all portrait), agent-written script/meta —
  no external LLM API billing.
- cost_estimate: $0 marginal (YouTube API free quota; local TTS/ffmpeg;
  media via existing pipeline).
- notes: topic #6 "Wombats poop cubes, and scientists finally figured out
  how"; recorded experiment arm hook=bold_claim+caption=off (arm label
  flipped between controller re-runs; DB records final arm as
  hook=bold_claim+caption=off). Factual claims verified by web search before
  scripting: wombats are the only animals with cube-shaped poop; cubes form
  in the last ~17% of the intestine where uneven wall stiffness (stretchy vs
  stiff regions) contracts at different speeds, molding flat faces and sharp
  corners (Patricia Yang / Georgia Tech, published in Soft Matter); up to
  ~100 cubes per night used to mark territory since cubes don't roll off
  rocks. Post-upload verification via videos.list: channelId
  UC7_uE-eclKr2rgryRV6A4QA, privacyStatus public, title matches — PASS.
