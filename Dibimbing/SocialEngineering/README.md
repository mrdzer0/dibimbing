# SEToolkit & GoPhish Cheatsheet

> **Scope:** Authorized phishing simulation, internal security assessment, awareness exercise, and red-team activity only.

---

# 1. Quick Comparison

| Tool                       | Fokus                                                 | Cocok untuk                                                          |
| -------------------------- | ----------------------------------------------------- | -------------------------------------------------------------------- |
| **SEToolkit / SET**        | Social engineering toolkit dengan workflow interaktif | Quick lab, cloning page, payload/social engineering testing          |
| **GoPhish**                | Phishing campaign management                          | Internal phishing simulation, tracking delivery/open/click/reporting |
| **GoPhish + SMTP Relay**   | Campaign + email delivery                             | Enterprise phishing simulation                                       |
| **GoPhish + Landing Page** | Tracking interaction                                  | Awareness testing dan red-team exercise                              |

---

# 2. SEToolkit

## Installation

### Kali Linux

Biasanya SET sudah tersedia:

```bash
sudo setoolkit
```

Jika belum:

```bash
sudo apt update
sudo apt install set
```

Check:

```bash
which setoolkit
```

atau:

```bash
setoolkit --help
```

---

# 4. Starting SEToolkit

```bash
sudo setoolkit
```

Main menu biasanya memiliki opsi seperti:

```text
1) Social-Engineering Attacks
2) Penetration Testing
3) Third Party Modules
4) Update the Social-Engineer Toolkit
```

Untuk phishing/social engineering simulation:

```text
1) Social-Engineering Attacks
```

Kemudian biasanya tersedia:

```text
1) Spear-Phishing Attack Vectors
2) Website Attack Vectors
3) Infectious Media Generator
4) Create a Payload and Listener
5) Mass Mailer Attack
```

---

# 5. SET Website Attack Vector

Flow umum:

```text
Social-Engineering Attacks
        ↓
Website Attack Vectors
        ↓
Credential Harvester / Web Template
        ↓
Clone / Custom Page
        ↓
Host Landing Page
```

Start:

```bash
sudo setoolkit
```

Pilih:

```text
1) Social-Engineering Attacks
2) Website Attack Vectors
```

Untuk simulation yang hanya mengevaluasi interaction/click, gunakan landing page dummy dan **hindari mengumpulkan password asli pengguna**.

---

# 6. SET Site Cloner

Typical flow:

```text
Website Attack Vectors
        ↓
Site Cloner
        ↓
Input Authorized URL
        ↓
SET creates local copy
        ↓
Serve locally
```

Contoh penggunaan untuk lab:

```text
URL:

https://training.example.internal
```

SET kemudian membuat landing page berdasarkan website tersebut.

Pastikan domain yang digunakan:

```text
- Milik organisasi
- Environment staging
- Training domain
- Explicitly authorized
```

---

# 7. SET Web Server

Check port:

```bash
sudo ss -lntp
```

atau:

```bash
sudo netstat -lntp
```

Contoh:

```text
0.0.0.0:80
0.0.0.0:443
```

Check local page:

```bash
curl http://127.0.0.1
```

---

# 8. SET Logs

Lokasi dapat berbeda tergantung versi/configuration.

Search:

```bash
sudo find /root/.set -type f 2>/dev/null
```

atau:

```bash
find ~/.set -type f 2>/dev/null
```

Check SET configuration:

```bash
cat /etc/setoolkit/set.config
```

Search relevant options:

```bash
grep -Ei 'WEB|PORT|APACHE|LOG' /etc/setoolkit/set.config
```

---

# 9. Useful SET Configuration

Config utama:

```bash
sudo nano /etc/setoolkit/set.config
```

Backup terlebih dahulu:

```bash
sudo cp /etc/setoolkit/set.config \
/etc/setoolkit/set.config.bak
```

Search configuration:

```bash
grep -v '^#' /etc/setoolkit/set.config | grep -v '^$'
```

---

# 10. GoPhish

## Download / Install

Extract binary:

```bash
unzip gophish*.zip
```

Masuk ke directory:

```bash
cd gophish
```

Check:

```bash
ls -lah
```

Typical files:

```text
gophish
config.json
static/
templates/
```

Give executable permission:

```bash
chmod +x gophish
```

Run:

```bash
sudo ./gophish
```

---

# 11. GoPhish Default Services

GoPhish umumnya mempunyai:

```text
Admin UI
Landing / Phishing Server
```

Check listener:

```bash
ss -lntp | grep gophish
```

Typical administration URL:

```text
https://127.0.0.1:3333
```

Check config:

```bash
cat config.json
```

Contoh struktur:

```json
{
    "admin_server": {
        "listen_url": "127.0.0.1:3333",
        "use_tls": true
    },
    "phish_server": {
        "listen_url": "0.0.0.0:80",
        "use_tls": false
    }
}
```

---

# 12. GoPhish Main Components

GoPhish campaign membutuhkan:

```text
Users & Groups
      +
Email Template
      +
Landing Page
      +
Sending Profile
      =
Campaign
```

Flow:

```text
Create Group
    ↓
Create Sending Profile
    ↓
Create Email Template
    ↓
Create Landing Page
    ↓
Create Campaign
    ↓
Launch
    ↓
Monitor Results
```

---

# 13. Users & Groups

Menu:

```text
Users & Groups
```

Add users manually atau import CSV.

Example CSV:

```csv
First Name,Last Name,Position,Email
John,Doe,Engineer,john.doe@example.com
Jane,Doe,Finance,jane.doe@example.com
```

Pastikan seluruh recipient termasuk:

```text
Authorized phishing simulation scope
```

---

# 14. Sending Profile

Menu:

```text
Sending Profiles
```

Required information:

```text
Name
SMTP From
Host
Username
Password
```

Example internal relay:

```text
SMTP From:

security-awareness@example.com

Host:

smtp.example.internal:587
```

Recommended:

```text
Use dedicated simulation SMTP account
```

Hindari menggunakan personal mailbox.

---

# 15. Test SMTP Profile

GoPhish memiliki:

```text
Send Test Email
```

Sebelum campaign:

```text
Sending Profiles
    ↓
Select Profile
    ↓
Send Test Email
```

Pastikan:

```text
Email delivered
SPF accepted
DKIM accepted
DMARC behavior understood
Tracking URL reachable
```

---

# 16. Email Template

Menu:

```text
Email Templates
```

Contoh template awareness:

```html
<html>
<body>

<p>Hello {{.FirstName}},</p>

<p>
There is a security notification requiring your attention.
</p>

<p>
<a href="{{.URL}}">
Review Notification
</a>
</p>

<p>
Security Operations
</p>

</body>
</html>
```

Important GoPhish variable:

```text
{{.FirstName}}
{{.LastName}}
{{.Email}}
{{.Position}}
{{.URL}}
```

Yang paling penting untuk tracking:

```text
{{.URL}}
```

---

# 17. Landing Page

Menu:

```text
Landing Pages
```

Landing page dapat dibuat manual.

Example:

```html
<html>

<head>
<title>Security Awareness Exercise</title>
</head>

<body>

<h2>Security Awareness Simulation</h2>

<p>
This page is part of an authorized phishing simulation.
</p>

<p>
No password has been collected.
</p>

</body>

</html>
```

Recommended untuk awareness campaign:

```text
User clicks
    ↓
Show training message
    ↓
Explain phishing indicator
```

---

# 18. Import Existing Page

GoPhish menyediakan fitur:

```text
Import Site
```

Gunakan hanya pada:

```text
Authorized internal site
Training site
Staging environment
Owned domain
```

---

# 19. Campaign Creation

Menu:

```text
Campaigns
    ↓
New Campaign
```

Isi:

```text
Name
Email Template
Landing Page
URL
Sending Profile
Groups
```

Example:

```text
Campaign Name:

Q3 Security Awareness Simulation
```

Campaign URL:

```text
https://training.example.com
```

---

# 20. Recommended Campaign Flow

```text
Prepare Domain
      ↓
Prepare TLS
      ↓
Configure SMTP
      ↓
Test Email
      ↓
Create Landing Page
      ↓
Create Email Template
      ↓
Create Test Group
      ↓
Internal Pilot
      ↓
Production Campaign
      ↓
Collect Metrics
      ↓
Awareness / Debrief
```

---

# 21. GoPhish Tracking

GoPhish dapat mengukur:

```text
Email Sent

Email Opened

Link Clicked

Interaction Submitted

Email Reported
```

Untuk campaign awareness, metrik yang paling berguna:

```text
Delivery Rate

Open Rate

Click Rate

Report Rate

Time-to-Report
```

---

# 22. Useful Metrics

## Delivery Rate

```text
Delivered / Sent × 100
```

Example:

```text
950 / 1000 × 100

= 95%
```

---

## Click Rate

```text
Clicked / Delivered × 100
```

Example:

```text
120 / 950 × 100

= 12.63%
```

---

## Report Rate

```text
Reported / Delivered × 100
```

---

## Reporting Effectiveness

Useful comparison:

```text
Reported Users
      vs
Clicked Users
```

Ideal trend:

```text
Click Rate ↓
Report Rate ↑
```

---

# 23. Suggested Campaign Metrics

Minimal dashboard:

| Metric               | Purpose                 |
| -------------------- | ----------------------- |
| Emails Sent          | Total target            |
| Delivered            | Delivery success        |
| Opened               | User interaction        |
| Clicked              | Susceptibility          |
| Reported             | Security awareness      |
| Failed Delivery      | SMTP/address issue      |
| Time to First Report | Detection effectiveness |

---

# 24. GoPhish Process Management

Run foreground:

```bash
sudo ./gophish
```

Run temporary background:

```bash
nohup ./gophish > gophish.log 2>&1 &
```

Check:

```bash
ps aux | grep gophish
```

Stop:

```bash
pkill gophish
```

Check logs:

```bash
tail -f gophish.log
```

---

# 25. systemd Service

Example:

```bash
sudo nano /etc/systemd/system/gophish.service
```

Content:

```ini
[Unit]
Description=GoPhish
After=network.target

[Service]
Type=simple
WorkingDirectory=/opt/gophish
ExecStart=/opt/gophish/gophish
Restart=always

[Install]
WantedBy=multi-user.target
```

Reload:

```bash
sudo systemctl daemon-reload
```

Enable:

```bash
sudo systemctl enable gophish
```

Start:

```bash
sudo systemctl start gophish
```

Status:

```bash
sudo systemctl status gophish
```

Logs:

```bash
sudo journalctl -u gophish
```

Live:

```bash
sudo journalctl -u gophish -f
```

---

# 26. Reverse Proxy

Typical architecture:

```text
Internet / Internal User
        ↓
      Nginx
        ↓
     GoPhish
```

Check nginx:

```bash
sudo nginx -t
```

Reload:

```bash
sudo systemctl reload nginx
```

---

# 27. DNS Preparation

Typical records:

```text
training.example.com
        ↓
       A
        ↓
GoPhish Server
```

Check:

```bash
dig training.example.com
```

Short result:

```bash
dig +short training.example.com
```

Check from client:

```bash
nslookup training.example.com
```

---

# 28. TLS

Recommended:

```text
HTTPS Landing Page
```

Check certificate:

```bash
openssl s_client \
-connect training.example.com:443 \
-servername training.example.com
```

Quick curl:

```bash
curl -I https://training.example.com
```

---

# 29. SMTP Troubleshooting

Test port:

```bash
nc -vz smtp.example.com 587
```

atau:

```bash
telnet smtp.example.com 587
```

TLS:

```bash
openssl s_client \
-starttls smtp \
-connect smtp.example.com:587
```

Check DNS:

```bash
dig MX example.com
```

---

# 30. SPF

Check:

```bash
dig TXT example.com
```

Search:

```bash
dig TXT example.com | grep spf
```

Typical:

```text
v=spf1 include:mail.example.com ~all
```

---

# 31. DMARC

Check:

```bash
dig TXT _dmarc.example.com
```

Typical:

```text
v=DMARC1; p=none;
```

---

# 32. DKIM

Example:

```bash
dig TXT selector1._domainkey.example.com
```

Selector tergantung mail infrastructure.

---

# 33. Mail Delivery Troubleshooting

Check:

```text
SMTP authentication
SMTP relay permissions
SPF
DKIM
DMARC
Recipient filtering
Secure email gateway
Anti-spam
URL filtering
Domain reputation
```

---

# 34. Landing Page Troubleshooting

Check DNS:

```bash
dig +short training.example.com
```

Check port:

```bash
nc -vz training.example.com 443
```

Check HTTP:

```bash
curl -vk https://training.example.com
```

Check GoPhish listener:

```bash
ss -lntp
```

Check reverse proxy:

```bash
sudo nginx -t
```

---

# 35. Validate Tracking URL

Email template harus menggunakan:

```text
{{.URL}}
```

Bukan hardcoded:

```text
https://training.example.com
```

Karena GoPhish membutuhkan campaign-specific tracking identifier.

Correct:

```html
<a href="{{.URL}}">
View Notification
</a>
```

---

# 36. Pilot Campaign

Sebelum campaign besar gunakan:

```text
3–10 internal security team users
```

Test:

```text
Email received
      ↓
Tracking works
      ↓
Landing page works
      ↓
TLS valid
      ↓
No broken images
      ↓
Reporting works
      ↓
Metrics recorded
```

---

# 37. Recommended Campaign Scope

Document:

```text
Campaign Owner

Security Approver

Target Department

Number of Users

Start Time

End Time

Simulation Scenario

Landing Domain

Sender Domain

SMTP Infrastructure

Allowed Techniques

Prohibited Techniques

Data Retention

Reporting Method
```

---

# 38. Safety Guardrails

Recommended restrictions:

```text
DO NOT collect real employee passwords

DO NOT reuse submitted credentials

DO NOT request MFA/OTP

DO NOT impersonate emergency/public safety authorities

DO NOT trigger financial transactions

DO NOT target personal email accounts

DO NOT deploy malware unless explicitly authorized

DO NOT automatically execute downloaded payloads

DO NOT retain unnecessary personal information
```

---

# 39. Safer Credential Simulation

Instead of storing actual password:

```text
Username entered: YES
Password field used: YES
Password value stored: NO
```

You generally only need:

```text
User interacted with login form
```

rather than:

```text
Actual credential
```

---

# 40. Whitelisting

Coordinate with:

```text
SOC
Email Team
Network Team
Security Gateway Team
Infrastructure
Incident Response
```

Potential whitelist:

```text
Sender address

Sender domain

SMTP server IP

Landing page domain

Landing server IP
```

However, avoid bypassing **all security controls** if the purpose of the exercise includes evaluating:

```text
Email Security Gateway
URL filtering
EDR
SOC detection
```

---

# 41. Two Common Simulation Models

## Awareness Focused

```text
Security Controls Whitelisted
            ↓
Evaluate Human Behavior
```

Objective:

```text
Click Rate
Report Rate
User Awareness
```

---

## Red-Team Focused

```text
Minimal Whitelisting
        ↓
Evaluate Security Stack
        +
Human Detection
```

Objective:

```text
Email Gateway Detection

SOC Detection

User Reporting

Incident Response

Domain / URL Detection
```

---

# 42. SEToolkit vs GoPhish Workflow

## SEToolkit

```text
sudo setoolkit

        ↓

Social Engineering Attacks

        ↓

Website Attack Vectors

        ↓

Create / Clone Training Page

        ↓

Test locally
```

Best for:

```text
Lab

Quick PoC

Landing page experiment

Social engineering testing
```

---

## GoPhish

```text
Users & Groups
      ↓
Sending Profile
      ↓
Email Template
      ↓
Landing Page
      ↓
Campaign
      ↓
Metrics
```

Best for:

```text
Enterprise Phishing Simulation

Awareness Campaign

Repeatable Campaign

Metrics / Reporting
```

---

# 43. Recommended Production Setup

```text
                    ┌───────────────┐
                    │  Admin User   │
                    └───────┬───────┘
                            │
                            ▼
                   HTTPS :3333
                            │
                     ┌──────▼──────┐
                     │   GoPhish   │
                     └──────┬──────┘
                            │
             ┌──────────────┴───────────────┐
             │                              │
             ▼                              ▼
        SMTP Relay                       Nginx
                                              │
                                              ▼
                                           HTTPS
                                              │
                                              ▼
                                        Landing Page
```

Admin interface sebaiknya:

```text
127.0.0.1

atau

Internal Management Network
```

Jangan expose:

```text
GoPhish Admin UI
```

langsung ke internet.

---

# 44. Basic Security Hardening

GoPhish host:

```bash
sudo apt update
sudo apt upgrade
```

Firewall:

```bash
sudo ufw allow 22/tcp
sudo ufw allow 80/tcp
sudo ufw allow 443/tcp
```

Example admin restriction:

```text
3333/tcp

Internal / localhost only
```

Check:

```bash
sudo ufw status
```

---

# 45. Useful Linux Commands

Process:

```bash
ps aux | grep gophish
```

Ports:

```bash
ss -lntp
```

DNS:

```bash
dig +short training.example.com
```

HTTP:

```bash
curl -I https://training.example.com
```

Logs:

```bash
tail -f gophish.log
```

Service:

```bash
systemctl status gophish
```

Firewall:

```bash
ufw status
```

---

# 46. Pre-Campaign Checklist

```text
[ ] Written authorization obtained

[ ] Scope approved

[ ] Target group confirmed

[ ] Sender domain prepared

[ ] Landing domain prepared

[ ] DNS working

[ ] TLS working

[ ] SMTP tested

[ ] SPF configured

[ ] DKIM checked

[ ] DMARC behavior checked

[ ] Landing page tested

[ ] Tracking tested

[ ] Internal pilot completed

[ ] SOC informed according to exercise design

[ ] HR / Legal approval if required

[ ] Data retention defined

[ ] Emergency stop procedure prepared
```

---

# 47. During Campaign Checklist

```text
[ ] SMTP delivery monitored

[ ] Landing page availability monitored

[ ] GoPhish logs monitored

[ ] SOC escalation monitored

[ ] User reporting monitored

[ ] Unexpected impact monitored

[ ] Stop campaign if business impact occurs
```

---

# 48. Post-Campaign Checklist

```text
[ ] Stop campaign

[ ] Disable landing page

[ ] Export statistics

[ ] Remove unnecessary personal data

[ ] Calculate click rate

[ ] Calculate report rate

[ ] Analyze time-to-report

[ ] Identify security-control detections

[ ] Conduct awareness debrief

[ ] Produce management report

[ ] Record lessons learned
```

---

# 49. Suggested Executive Report

```text
Phishing Simulation
===================

Campaign:
Q3 Security Awareness Exercise

Targets:
500 employees

Delivery Rate:
97%

Open Rate:
65%

Click Rate:
11%

Report Rate:
32%

Median Time to Report:
8 minutes

Security Control Result:
Email Gateway: Detected partially
EDR: N/A
SOC: Detected
User Reporting: Effective

Key Observation:
Users demonstrated good reporting behavior,
although click rate remains above the target.

Recommendation:
Conduct targeted awareness training for
high-risk departments and repeat simulation
within the next quarter.
```

---

# 50. Quick Reference

## SEToolkit

Start:

```bash
sudo setoolkit
```

Config:

```bash
cat /etc/setoolkit/set.config
```

SET files:

```bash
find ~/.set -type f
```

Ports:

```bash
ss -lntp
```

---

## GoPhish

Start:

```bash
./gophish
```

Background:

```bash
nohup ./gophish > gophish.log 2>&1 &
```

Logs:

```bash
tail -f gophish.log
```

Process:

```bash
ps aux | grep gophish
```

Ports:

```bash
ss -lntp
```

Admin:

```text
https://127.0.0.1:3333
```

Configuration:

```bash
cat config.json
```

---

# 51. Recommended GoPhish Order

Memorize:

```text
GROUP
  ↓
SMTP
  ↓
TEMPLATE
  ↓
LANDING PAGE
  ↓
CAMPAIGN
  ↓
RESULT
```

Or:

```text
Who
 ↓
How to Send
 ↓
What Email
 ↓
Where Click Goes
 ↓
Launch
 ↓
Measure
```

---

# 52. Troubleshooting Flow

If email does not arrive:

```text
GoPhish
   ↓
SMTP Credentials
   ↓
SMTP Relay
   ↓
SPF / DKIM / DMARC
   ↓
Email Gateway
   ↓
Mailbox
```

If landing page does not open:

```text
DNS
 ↓
Firewall
 ↓
Nginx
 ↓
TLS
 ↓
GoPhish Listener
 ↓
Landing Page
```

If click is not recorded:

```text
Email Template
      ↓
{{.URL}}
      ↓
Campaign URL
      ↓
GoPhish Tracking ID
      ↓
Landing Page
```

---

# 53. Minimal Command Cheatsheet

```bash
# SET
sudo setoolkit

# GoPhish
cd /opt/gophish
sudo ./gophish

# Process
ps aux | grep gophish

# Port
ss -lntp

# DNS
dig +short training.example.com

# HTTP
curl -I https://training.example.com

# SMTP
nc -vz smtp.example.com 587

# SMTP TLS
openssl s_client \
-starttls smtp \
-connect smtp.example.com:587

# SPF
dig TXT example.com

# DMARC
dig TXT _dmarc.example.com

# Logs
tail -f gophish.log

# Service
systemctl status gophish

# Firewall
ufw status
```


