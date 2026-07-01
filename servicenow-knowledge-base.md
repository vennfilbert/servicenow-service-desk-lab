# Knowledge Base

Six knowledge articles for common L1 service desk tasks, written as part of the
ServiceNow service desk lab. Each documents a real, standard procedure using the same
structure: Symptom, Cause, Resolution, Verification, and when to escalate.

---

# 1. Unlock a locked Active Directory account

**Article ID:** KB0010021
**Category:** Access
**Applies to:** Any standard staff AD account

## Symptom
User reports they cannot sign in and sees a message that their account is locked,
often after several wrong password attempts or an old password cached on a phone.

## Cause
The account passed the failed sign-in threshold and Active Directory locked it to
block a possible attack. A stale password saved on a mobile device or mapped drive is
a common trigger.

## Resolution
1. Verify the caller's identity against the agreed identity check.
2. Open Active Directory Users and Computers, find the user, open Properties, and on
   the Account tab clear the lock. Or run in PowerShell:
   `Unlock-ADAccount -Identity jsmith`
3. Ask the user to close any device that may be holding the old password (mail app on
   a phone is the usual culprit) before they try again.

## Verification
Have the user sign in successfully on their primary device while you are on the call.

## Escalate when
The account re-locks within minutes of unlocking. That points to a stale credential
somewhere you cannot see, or repeated targeting. Send to the identity or security
group with the lockout source if your tooling shows it.

## Related articles
Reset a user password in Active Directory

**Owner:** Service Desk  |  **Last reviewed:** 2026

---

# 2. Reset a user password in Active Directory

**Article ID:** KB0010022
**Category:** Access
**Applies to:** Any standard staff AD account

## Symptom
User has forgotten their password, or has been locked out repeatedly because the old
password is wrong.

## Cause
Forgotten or expired credential.

## Resolution
1. Verify the caller's identity against the agreed identity check. Do not skip this.
2. Reset the password. In Active Directory Users and Computers, right click the user
   and choose Reset Password. Or in PowerShell:
   `Set-ADAccountPassword -Identity jsmith -Reset`
   followed by
   `Set-ADUser -Identity jsmith -ChangePasswordAtLogon $true`
3. Give the temporary password to the user through a secure channel. Do not send it in
   plain email.

## Verification
User signs in with the temporary password and is prompted to set a new one. Confirm
the new sign-in works.

## Escalate when
The reset does not take effect across systems after a reasonable sync window, which
can point to a replication problem. Send to the directory services group.

## Related articles
Unlock a locked Active Directory account

**Owner:** Service Desk  |  **Last reviewed:** 2026

---

# 3. Connect to the corporate VPN and common failures

**Article ID:** KB0010023
**Category:** Network
**Applies to:** Staff connecting remotely through the corporate VPN client

## Symptom
A remote user cannot establish a VPN connection. The client fails, often after the
user enters their credentials, and they cannot reach internal systems.

## Cause
Most remote VPN failures at first contact come from one of a handful of causes: an
expired or locked account password, an out-of-date VPN client, an MFA prompt that was
not completed, or a client session that needs restarting. A smaller number are genuine
gateway or configuration faults, which are not an L1 fix.

## Resolution
1. Verify the caller's identity against the agreed identity check.
2. Confirm the account is active and not locked, and that the password is current. An
   expired or locked credential is the most common cause. Reset or unlock if needed.
3. Confirm the VPN client is on the current supported version. Update it if it is out
   of date.
4. Confirm the multi-factor prompt is completing. Ask the user to watch for the push
   or code and approve it.
5. Have the user fully close and reopen the VPN client, then retry the connection.

## Verification
User connects to the VPN and can reach an internal resource (for example a shared
drive or intranet page) while you are on the call.

## Escalate when
The connection still fails after the account, client, MFA, and restart checks. That
points to a VPN gateway or configuration fault beyond L1 scope. Escalate to the Network
team with your troubleshooting steps recorded in the work notes.

## Related articles
Unlock a locked Active Directory account
Reset a user password in Active Directory

**Owner:** Service Desk  |  **Last reviewed:** 2026

---

# 4. Repair a corrupted Outlook profile

**Article ID:** KB0010024
**Category:** Email
**Applies to:** Users running the Outlook desktop client on Windows

## Symptom
Outlook will not open, closes on launch, or hangs on the loading screen. The user can
usually still reach their email through webmail in the browser.

## Cause
A corrupted Outlook mail profile, a faulty add-in, or a damaged local data file. These
are local client problems, not a mailbox or server issue, which is why webmail still
works.

## Resolution
1. Verify the caller's identity against the agreed identity check.
2. Start Outlook in safe mode to rule out a faulty add-in (hold Ctrl while launching
   Outlook, or run `outlook.exe /safe`). If it opens in safe mode, disable add-ins one
   at a time to find the culprit.
3. If safe mode does not resolve it, recreate the mail profile through Mail settings in
   Control Panel: create a new profile, add the user's account, and set the new profile
   as default.
4. If the problem persists, run an Office repair (Quick Repair first, then Online
   Repair if needed).

## Verification
Outlook launches normally in standard mode and the mailbox loads. Confirm with the
user that they can send and receive.

## Escalate when
The client still fails after a profile rebuild and Office repair, or the issue affects
multiple users at once (which suggests a mail server or Exchange problem rather than a
local one). Escalate to the messaging or email support team.

## Related articles
Automatic Replies (Out Of Office)

**Owner:** Service Desk  |  **Last reviewed:** 2026

---

# 5. Request and grant shared drive access

**Article ID:** KB0010025
**Category:** Access
**Applies to:** Staff requesting access to a team or department shared drive

## Symptom
A user requests access to a shared drive or folder they cannot currently reach, or
reports "access denied" when opening a network location they should be able to use.

## Cause
The user is not a member of the Active Directory security group that controls
permissions for that shared folder.

## Resolution
1. Verify the caller's identity against the agreed identity check.
2. Confirm the request has manager or data owner approval before granting anything. Do
   not add access on the user's request alone. Record who approved it.
3. Identify the correct AD security group that governs the folder.
4. Add the user to that security group. In Active Directory Users and Computers, add
   the member to the group, or in PowerShell:
   `Add-ADGroupMember -Identity "GroupName" -Members jsmith`
5. Ask the user to sign out and back in (group membership refreshes at next logon) then
   confirm they can open the folder.

## Verification
User can open the shared folder and access its contents after signing back in.

## Escalate when
The correct group is unclear, the folder has non-standard or broken permissions, or the
request is for a restricted area needing higher approval. Escalate to the team that owns
the file server or the data owner.

## Related articles
Onboard a new starter, account and access checklist

**Owner:** Service Desk  |  **Last reviewed:** 2026

---

# 6. Onboard a new starter, account and access checklist

**Article ID:** KB0010026
**Category:** Onboarding
**Applies to:** Provisioning accounts and access for a new employee

## Symptom
A new employee is starting and needs their accounts and access set up before their
first day. Comes in as an onboarding service request, usually from a manager or HR.

## Cause
Standard onboarding. No fault to fix, this is scheduled provisioning work.

## Resolution
1. Confirm the request details and that it has proper approval (manager or HR).
2. Create the Active Directory account in the correct department organisational unit
   (OU), using the standard naming convention.
3. Add the user to the department security groups that grant their standard access.
4. Provision the mailbox and assign the required licence.
5. Grant the standard shared drive access for that team (via the relevant security
   groups).
6. Record the temporary password and pass it to the new starter or their manager
   through a secure channel.

## Verification
New starter can sign in, reach their email, and open the shared resources their role
requires. Confirm before closing the request.

## Escalate when
The request needs non-standard access, application accounts your team does not manage,
or hardware that another team provisions. Route those parts to the correct team and
track them to completion.

## Related articles
Reset a user password in Active Directory
Request and grant shared drive access

**Owner:** Service Desk  |  **Last reviewed:** 2026
