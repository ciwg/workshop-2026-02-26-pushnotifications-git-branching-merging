class: center, middle

# Push Notifications & Git Branching

**Tools for your development workflow**

JJ Salley

---

## Outline

1. Push Notifications — Why & How
2. ntfy — Free Push Notifications
3. Twilio — SMS Notifications
4. Git Branching & Merging
5. Demo
6. Practice Resources

---

## Push Notifications

- We need real-time alerts: deploys, CI failures, commits, incidents
- Every phone push notification must go through Google (Android) or Apple (iPhone)
- Building our own app for this is not practical
- SMS requires carrier registration (10DLC), per-message costs, and weeks of approval

--

### Two approaches we'll cover:

- **ntfy** — free, open-source push notifications via an app
- **Twilio** — SMS to any phone, no app required

---


## What is ntfy?

- Free — no API key, no account, no per-message cost
- 250 messages/day on the free tier
- Self-hostable if we need more

## How It Works

1. Install the ntfy app (Android / iOS)
2. Subscribe to a topic
3. Any HTTP POST to that topic → push notification on your phone

---

## Live Demo — Subscribe Now

**Topic:** `nfty-test-jj-2026`

**App:** search "ntfy" in your app store

**Browser:** https://ntfy.sh/nfty-test-jj-2026

---

## Demo: Basic Alert

```
echo "deploy complete" | ./nfty-test -topic nfty-test-jj-2026
```

---

## Demo: Critical Alert

```
echo "prod is down" | ./nfty-test -topic nfty-test-jj-2026 \
  -title "ALERT" -priority max -tags rotating_light
```

Your phone will vibrate.

---

## Demo: Git Commits

```
git log --oneline -3 | ./nfty-test -topic nfty-test-jj-2026 \
  -batch -repo . -title "Recent Commits"
```

Tap the notification → opens the commit on GitHub/Gitea.

---

## What We Could Use ntfy For

- CI/CD pipeline notifications
- Deploy alerts
- Monitoring / uptime alerts
- Commit and PR activity
- One topic per tool — subscribe to what you care about

---

# SMS Notifications with Twilio

---

## Why Twilio?

- SMS reaches any phone — no app install required
- Same CLI pattern as nfty-test
- Reads from stdin, sends SMS per line or batched

---

## What You Need


- Twilio account (free trial gives ~$15 credit)
- A Twilio phone number (~$1.15/month)
- Toll-Free Verification or A2P 10DLC registration before messages will deliver

---

## Setup

```
export TWILIO_ACCOUNT_SID="ACxxxxxxxx..."
export TWILIO_AUTH_TOKEN="your_auth_token"
export TWILIO_FROM="+18001234567"
```

---

## How to Use It

```
echo "Hello from the demo!" | ./twillio-test -to +14257999227
```

| Flag | What It Does |
|------|-------------|
| `-to` | Recipient phone number (required) |
| `-title` | Add a title line to the SMS |
| `-batch` | Combine all input into one SMS |

---

## Twilio Demo


```
echo "Hello from the demo!" | ./twillio-test -to +14257999227

```

---

## Twilio vs ntfy

| | ntfy | Twilio |
|---|------|--------|
| Delivery | Push notification (app) | SMS (any phone) |
| Cost | Free | ~$0.008/message |
| Setup | None | Account + number + registration |
| App required | Yes | No |

---

## Carrier Registration

- **Toll-Free numbers** → Toll-Free Verification (free, days to approve)
- **Local numbers** → A2P 10DLC registration (~$19 fees, days to approve)
- Without registration, messages show as **Undelivered**

---

## Next Steps for Notifications

- Pick topic names for our tools
- Integrate into CI/CD pipelines
- Evaluate self-hosting if we outgrow the free tier
- Repos:
  - https://github.com/computerscienceiscool/nfty-test
  - https://github.com/computerscienceiscool/twillio-test

---

# Git Branching & Merging

---

## Why Branch?

- Work on features without breaking `main`
- Multiple people can work in parallel
- Review changes before merging via Pull Requests

--

---

class: center, middle

 #Demo

---

## Want to Practice?

Fork and clone this repo to practice on your own:

**https://github.com/computerscienceiscool/git-practice-repo**

- Cheatsheet, walkthrough, and practice files included
- Each section is independent — do them in any order

---

class: center, middle

# Thank You!

