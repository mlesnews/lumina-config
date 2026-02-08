# Outlook Classic - Quick Setup Card

## 🎯 Goal
Connect Outlook Classic to NAS Mail Hub to receive all emails (Gmail + ProtonMail + Company)

---

## ⚡ Quick Setup Steps

### 1. Open Outlook Account Settings
- **File** → **Account Settings** → **Account Settings**

### 2. Add New Account
- Click **New...**
- Select **Manual setup or additional server types**
- Click **Next**
- Select **POP or IMAP**
- Click **Next**

### 3. Enter These Exact Settings

**User Information:**
- **Your Name:** [Your Name]
- **Email Address:** `mlesn@homelab.lesnewski.local`

**Server Information:**
- **Account Type:** `IMAP` (select from dropdown)
- **Incoming mail server:** `10.17.17.32`
- **Outgoing mail server (SMTP):** `10.17.17.32`

**Logon Information:**
- **User Name:** `mlesn@homelab.lesnewski.local`
- **Password:** [Your NAS Mail Hub password]

### 4. Advanced Settings

Click **More Settings...**

**Outgoing Server Tab:**
- ☑️ Check **"My outgoing server (SMTP) requires authentication"**
- Select **"Use same settings as my incoming mail server"**

**Advanced Tab:**
- **Incoming server (IMAP):**
  - Port: `993`
  - ☑️ **"This server requires an encrypted connection (SSL/TLS)"**
  - Encryption: `SSL/TLS`
- **Outgoing server (SMTP):**
  - Port: `587`
  - ☑️ **"This server requires an encrypted connection"**
  - Encryption: `STARTTLS`
- Click **OK**

### 5. Test & Finish
- Click **Next** (Outlook will test connection)
- If successful, click **Finish**

---

## ✅ Verification

1. Check Account Settings:
   - Should see: `mlesn@homelab.lesnewski.local`
   - Type: IMAP

2. Check Inbox:
   - Should see emails from Gmail, ProtonMail, and Company

3. Test Send/Receive:
   - Press **F9** to sync
   - Check for new emails

---

## 🔧 Settings Summary

| Setting | Value |
|---------|-------|
| Email | mlesn@homelab.lesnewski.local |
| Account Type | IMAP |
| Incoming Server | 10.17.17.32 |
| Incoming Port | 993 |
| Incoming Encryption | SSL/TLS |
| Outgoing Server | 10.17.17.32 |
| Outgoing Port | 587 |
| Outgoing Encryption | STARTTLS |
| Username | mlesn@homelab.lesnewski.local |
| Authentication | Required (same as incoming) |

---

## 🚨 Troubleshooting

**Can't connect?**
- Verify NAS Mail Hub is running: https://10.17.17.32:5001/mailplus
- Check network: `ping 10.17.17.32`
- Verify firewall allows ports 993 and 587

**Wrong password?**
- Verify password in NAS Mail Hub webmail
- Check username: `mlesn@homelab.lesnewski.local`

**No emails?**
- Run email import: `python scripts/python/import_emails_to_nas_hub.py --days-back 365`
- Check NAS Mail Hub webmail for emails
- Press F9 in Outlook to sync

---

**For detailed instructions:** See `OUTLOOK_DETAILED_SETUP_GUIDE.md`
