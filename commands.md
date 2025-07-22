# Sending Wazuh Email Alerts via Gmail Using `msmtp`

This guide shows how to send Wazuh alerts via Gmail by configuring `msmtp`.

> ⚠️ This assumes you're using Gmail.

---

## Step 1: Install Required Packages

Open your terminal and run:

```bash
sudo apt update
sudo apt install msmtp msmtp-mta mailutils -y
```

This installs the Gmail relay service that Wazuh will use.

---

## Step 2: Create the `msmtp` Config File

Run this command to open the config file in an editor:

```bash
sudo nano ~/.msmtprc
```

Paste this into the blank file:

```ini
default
auth           on
tls            on
tls_trust_file /etc/ssl/certs/ca-certificates.crt
logfile        ~/.msmtp.log

account        gmail
host           smtp.gmail.com
port           587
from           your-email@gmail.com
user           your-email@gmail.com
password       your-app-password

account default: gmail
```

> Replace `your-email@gmail.com` and `your-app-password` with your actual Gmail address and [Gmail App Password](https://support.google.com/accounts/answer/185833?hl=en). This is because Wazuh email config doen't use the normal Gmail password.

Save and exit the file:  
- Press `CTRL + O`, then `Enter` to save.  
- Press `CTRL + X` to exit.

---

## Step 3: Fix Permissions

Run this to restrict the config file to only be accessible by you:

```bash
chmod 600 ~/.msmtprc
```

---

## Step 4: Test If It Works

Send a test email:

```bash
echo "Wazuh test email body" | mail -s "Test from Wazuh Server" recipient@gmail.com
```

> 📥 Check your Gmail inbox. If the email arrives, `msmtp` is working.

---

## ✅ Done

Wazuh is now set to send alerts via Gmail using `msmtp`.


