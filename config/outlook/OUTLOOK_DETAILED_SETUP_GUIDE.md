# Outlook Classic Setup - NAS Mail Hub (Detailed Guide)

## Prerequisites

- ✅ Microsoft Outlook (Classic/Desktop) installed
- ✅ NAS Mail Hub running (10.17.17.32)
- ✅ Company email account: mlesn@homelab.lesnewski.local
- ✅ NAS Mail Hub password

---

## Step-by-Step Setup

### Step 1: Open Outlook Account Settings

1. **Open Microsoft Outlook**
2. Click **File** (top-left menu)
3. Click **Account Settings** → **Account Settings...**
   - This opens the Account Settings dialog

### Step 2: Add New Account

1. In the **Account Settings** dialog, click **New...** button
2. Select **Manual setup or additional server types**
3. Click **Next >**

### Step 3: Choose Account Type

1. Select **POP or IMAP**
2. Click **Next >**

### Step 4: Enter Account Information

Fill in the following information:

**User Information:**
- **Your Name:** Your Display Name (e.g., "Your Name")
- **Email Address:** `mlesn@homelab.lesnewski.local`

**Server Information:**
- **Account Type:** Select **IMAP** from dropdown
- **Incoming mail server:** `10.17.17.32`
- **Outgoing mail server (SMTP):** `10.17.17.32`

**Logon Information:**
- **User Name:** `mlesn@homelab.lesnewski.local`
- **Password:** [Enter your NAS Mail Hub password]
- ☑️ Check **"Remember password"** (optional)

### Step 5: Configure Advanced Settings

1. Click **More Settings...** button

#### Outgoing Server Tab

1. Click **Outgoing Server** tab
2. ☑️ Check **"My outgoing server (SMTP) requires authentication"**
3. Select **"Use same settings as my incoming mail server"**

#### Advanced Tab

1. Click **Advanced** tab
2. **Incoming server (IMAP):**
   - Port: `993`
   - ☑️ Check **"This server requires an encrypted connection (SSL/TLS)"**
   - Encryption: Select **SSL/TLS** from dropdown
3. **Outgoing server (SMTP):**
   - Port: `587`
   - ☑️ Check **"This server requires an encrypted connection"**
   - Encryption: Select **STARTTLS** from dropdown
4. Click **OK**

### Step 6: Test Connection

1. Click **Next >**
2. Outlook will test the connection:
   - ✅ **Green checkmarks** = Connection successful
   - ❌ **Red X** = Connection failed (see troubleshooting)

### Step 7: Complete Setup

1. If test is successful, click **Finish**
2. The account will appear in your Account Settings list
3. Click **Close** to exit Account Settings

---

## Verification

### Check Account in Outlook

1. Go to **File** → **Account Settings** → **Account Settings**
2. You should see: **mlesn@homelab.lesnewski.local** listed
3. Account Type should show: **IMAP**

### Check Email Sync

1. In Outlook, check your **Inbox**
2. You should see emails from:
   - Gmail (imported to NAS Mail Hub)
   - ProtonMail (imported to NAS Mail Hub)
   - Company email (direct to NAS Mail Hub)

### Check Folder Structure

1. In Outlook, expand the account folder
2. You should see standard IMAP folders:
   - Inbox
   - Sent Items
   - Drafts
   - Deleted Items
   - etc.

---

## Troubleshooting

### Connection Test Fails

**Error: "Cannot connect to server"**

**Solutions:**
1. Verify NAS Mail Hub is running:
   - Open: https://10.17.17.32:5001/mailplus
   - Log in and verify webmail works
2. Check network connectivity:
   - Ping: `ping 10.17.17.32`
   - Verify you're on the same network
3. Check firewall:
   - Ensure ports 993 (IMAP) and 587 (SMTP) are allowed
4. Verify server address:
   - Incoming: `10.17.17.32`
   - Outgoing: `10.17.17.32`

**Error: "Username and password not accepted"**

**Solutions:**
1. Verify username: `mlesn@homelab.lesnewski.local`
2. Verify password is correct for NAS Mail Hub
3. Check if account exists in NAS Mail Hub
4. Try logging into webmail with same credentials

**Error: "Cannot send email"**

**Solutions:**
1. Verify SMTP settings:
   - Server: `10.17.17.32`
   - Port: `587`
   - Encryption: STARTTLS
2. Verify "My outgoing server requires authentication" is checked
3. Verify "Use same settings as my incoming mail server" is selected

### No Emails Visible

**Issue: Outlook connected but no emails**

**Solutions:**
1. Verify email import is running:
   - Check: `data/email_import/` for import logs
   - Run: `python scripts/python/import_emails_to_nas_hub.py --days-back 7`
2. Check NAS Mail Hub webmail:
   - Verify emails are present in webmail
   - If not, run email import first
3. Check Outlook sync:
   - Right-click account → **Update Folder**
   - Or: **Send/Receive** → **Update Folder**

### Emails Not Syncing

**Issue: Emails not updating**

**Solutions:**
1. Check Outlook send/receive settings:
   - File → Options → Advanced → Send/Receive
   - Verify account is included in send/receive groups
2. Manually sync:
   - Press **F9** to send/receive
   - Or: **Send/Receive** → **Send/Receive All Folders**
3. Check account status:
   - File → Account Settings → Account Settings
   - Verify account shows as "Connected"

---

## Configuration Summary

### Account Settings
- **Email:** mlesn@homelab.lesnewski.local
- **Account Type:** IMAP
- **Display Name:** Your Name

### IMAP Settings
- **Server:** 10.17.17.32
- **Port:** 993
- **Encryption:** SSL/TLS
- **Username:** mlesn@homelab.lesnewski.local

### SMTP Settings
- **Server:** 10.17.17.32
- **Port:** 587
- **Encryption:** STARTTLS
- **Authentication:** Required (same as incoming)

---

## Next Steps After Setup

1. **Verify Email Import:**
   - Ensure Gmail and ProtonMail emails are being imported to NAS Mail Hub
   - Run: `python scripts/python/import_emails_to_nas_hub.py --days-back 365`

2. **Set Up Email Rules (Optional):**
   - Organize emails by source (Gmail, ProtonMail, Company)
   - Create folders and rules in Outlook

3. **Configure Send/Receive:**
   - Set up automatic send/receive schedule
   - File → Options → Advanced → Send/Receive

4. **Set Default Account (Optional):**
   - If you have multiple accounts, set NAS Mail Hub as default
   - File → Account Settings → Account Settings → Set as Default

---

## Support

If you continue to have issues:

1. **Check Setup Script:**
   - Run: `config/outlook/setup_outlook_nas_hub.bat`
   - This will verify Outlook is accessible

2. **Review Logs:**
   - Check email import logs: `data/email_import/`
   - Check Outlook connection status

3. **Verify NAS Mail Hub:**
   - Access webmail: https://10.17.17.32:5001/mailplus
   - Verify account exists and is accessible

---

**Last Updated:** 2026-01-05  
**Status:** Ready for Setup
