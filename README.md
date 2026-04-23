From 66bef1dc6026860cc1177672bda889c98db133e1 Mon Sep 17 00:00:00 2001
From: cxxxxc11 <216065364+cxxxxc11@users.noreply.github.com>
Date: Fri, 12 Sep 2025 22:27:59 +0300
Subject: [PATCH] attachments

import imaplib
import email
import os

# Account settings: update with your credentials
EMAIL_ACCOUNT = "78mshahrani@gmail.com"
PASSWORD = "YOUR_PASSWORD_OR_APP_PASSWORD"  # Replace with your
account password or app password if using two-factor authentication
IMAP_SERVER = "imap.gmail.com"
PHONE = "0562553391"  # This variable is not used for authentication

def download_attachments():
try:
# Connect to the email server using SSL
mail = imaplib.IMAP4_SSL(IMAP_SERVER)
mail.login(EMAIL_ACCOUNT, PASSWORD)
mail.select("inbox")

# Search for all emails in the inbox
typ, data = mail.search(None, "ALL")
mail_ids = data[0].split()

# Create a directory to save  if it doesn't exist
attachments_dir = "attachments"
if not os.path.exists(attachments_dir):
os.makedirs(attachments_dir)

# Iterate through each email and download attachments
for num in mail_ids:
typ, msg_data = mail.fetch(num, "(RFC822)")
msg = email.message_from_bytes(msg_data[0][1])

# Walk through the email parts
for part in msg.walk():
if part.get_content_maintype() == "multipart":
continue
if part.get("Content-Disposition") is None:
continue

filename = part.get_filename()
if filename:
filepath = os.path.join(attachments_dir, filename)
with open(filepath, "wb") as f:
f.write(part.get_payload(decode=True))
print(f"Downloaded: {filepath}")

mail.logout()
except Exception as e:
print("Error:", e)

if __name__ == "__main__":
download_attachments
---
 0 files changed, 0 insertions(+), 0 deletions(-)

--
Working Copy 6.3.5

