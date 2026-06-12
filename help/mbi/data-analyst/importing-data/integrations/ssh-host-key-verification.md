---
title: SSH host key verification
description: Learn how Commerce Intelligence enrolls SSH host keys, how to refresh them, troubleshoot errors, and when to contact Support for SSH tunnel connections.
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
topic_v2:
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
    internal-label: Data integration
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
    internal-label: Commerce Intelligence
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
    internal-label: Data Warehouse Manager
---
# SSH host key verification {#ssh-host-keys}

[!DNL Commerce Intelligence] uses strict SSH host key verification for encrypted (SSH tunnel) database connections, including [MySQL](mysql-via-ssh-tunnel.md), [MongoDB](mongodb-via-ssh-tunnel.md), and [PostgreSQL](postgresql.md).

During **[!UICONTROL Save & Test]**, the system enrolls the SSH bastion host keys for your connection and stores them securely per connection. After enrollment, replication and tunneling only succeed when the live bastion host keys match the enrolled keys.

This model improves security by blocking man-in-the-middle attacks and unexpected host changes. It also means that host key rotation, missing trust material, or infrastructure changes can surface as SSH host key errors on the connection instead of generic tunnel failures.

>[!NOTE]
>
>**Admin** means a user with Admin permissions on your [!DNL Commerce Intelligence] account, not your Adobe org console unless stated otherwise. Only Admins can run **[!UICONTROL Refresh SSH Host Keys]**. If you do not see this control, ask an Admin on your account to run the refresh or contact Adobe Support.

You do not edit, upload, or manage `known_hosts` files. Enrollment and refresh run on Adobe infrastructure assigned to your account.

>[!IMPORTANT]
>
>Host key rotation requires an Admin to run **[!UICONTROL Refresh SSH Host Keys]**. If bastion host keys changed or the bastion identity changed (hostname, IP, or port), running **[!UICONTROL Save & Test]** again or re-saving the connection does not update enrolled keys. The connection can keep failing until an Admin refreshes the host keys.

## Expected behavior for Save & Test {#save-and-test}

**[!UICONTROL Save & Test]** performs **initial SSH host key enrollment only**. It is conservative by design and does not rotate or overwrite keys that are already enrolled for the connection.

| Enrolled host key state | What Save & Test does |
| --- | --- |
| Host keys not yet enrolled | Scans the bastion host and port, enrolls the host keys, and stores them for this connection |
| Host keys already enrolled | Skips enrollment. Does not overwrite, rotate, or delete existing enrolled keys, even if live bastion keys no longer match |
| Enrolled keys missing, empty, or invalid | Does not repair invalid trust material by itself. An Admin must run **[!UICONTROL Refresh SSH Host Keys]** or contact Support if errors continue |

After a successful first enrollment, later **[!UICONTROL Save & Test]** runs validate credentials and connection settings but leave enrolled SSH host keys unchanged.

## Expected behavior for Refresh SSH Host Keys {#refresh-ssh-host-keys}

**[!UICONTROL Refresh SSH Host Keys]** updates enrolled SSH host keys when the bastion has changed or when trust material must be repaired. An Admin starts the refresh from the connection in **[!UICONTROL Data]** > **[!UICONTROL Connections]**.

The refresh runs asynchronously on Adobe infrastructure assigned to your account. [!DNL Commerce Intelligence] returns after the refresh is queued. It does not run the scan on your workstation.

A refresh **rewrites** enrolled host keys only when one of these conditions is true:

* Enrolled host keys are missing
* Enrolled host keys are empty
* Enrolled host keys cannot be read
* Enrolled host keys fail validation
* A new scan returns different host key lines than the enrolled keys
* Fingerprints from the scan and enrolled keys do not match

If enrolled keys are current and valid, the refresh completes without changing them.

>[!TIP]
>
>Run **[!UICONTROL Refresh SSH Host Keys]** after your team rotates SSH host keys on the bastion, changes the bastion hostname or IP, or replaces the SSH endpoint. Wait a few minutes, then run **[!UICONTROL Save & Test]** to confirm the connection.

## Expected behavior during account migration {#migration}

You do not trigger account migration. Adobe performs data-server moves during maintenance or scaling and copies enrolled SSH host keys so strict verification continues to work after the move.

After Adobe notifies you that migration is complete:

1. Run **[!UICONTROL Save & Test]** to confirm the connection. Enrollment should be skipped if keys were copied successfully.
1. If SSH host key errors persist, ask an Admin to run **[!UICONTROL Refresh SSH Host Keys]**, wait a few minutes, then run **[!UICONTROL Save & Test]** again.
1. Contact Adobe Support if errors continue after **[!UICONTROL Save & Test]** and up to two **[!UICONTROL Refresh SSH Host Keys]** attempts.

## SSH host key error messages {#ssh-host-key-errors}

Connection status shows a single user-friendly SSH host key message. Raw OpenSSH errors are not shown in the dashboard.

The following table maps common messages to likely causes and typical next steps.

| Message or status | What it means | Possible causes | Typical next step |
| --- | --- | --- | --- |
| SSH host key verification failed | The bastion host key does not match enrolled keys, or trust material is unusable | SSH host keys rotated on the bastion; bastion hostname, IP, or port changed; enrolled keys missing, empty, invalid, or unreadable | Confirm **Remote Address** and **SSH Port**. Ask your infrastructure team whether bastion host keys changed. Ask an Admin to run **[!UICONTROL Refresh SSH Host Keys]**, wait a few minutes, then run **[!UICONTROL Save & Test]** |
| SSH host keys could not be enrolled | **[!UICONTROL Save & Test]** could not scan or store bastion host keys | Bastion unreachable from Adobe infrastructure; DNS failure; firewall blocks [!DNL Commerce Intelligence] IP addresses; wrong **Remote Address** or **SSH Port**; host key scan failure on the bastion | Verify firewall allowlisting using the [!DNL Commerce Intelligence] IP addresses on the database credentials page. Confirm the bastion accepts SSH on the configured port. Correct connection fields and run **[!UICONTROL Save & Test]** again |
| SSH host keys are missing or invalid | Strict verification blocked the tunnel because enrolled trust material is absent or corrupt | First connection never completed enrollment; prior refresh failed; migration did not copy keys; issue on Adobe infrastructure | Ask an Admin to run **[!UICONTROL Refresh SSH Host Keys]**, then **[!UICONTROL Save & Test]**. Contact Support if the error persists |
| Refresh SSH host keys could not be completed | The refresh did not update enrolled keys | Network, DNS, or scan failure during refresh; issue on Adobe infrastructure | Wait several minutes. Ask an Admin to run **[!UICONTROL Refresh SSH Host Keys]** again (second attempt if the first failed). Confirm bastion reachability and allowlisting. Contact Support if the connection still fails after two refresh attempts and **[!UICONTROL Save & Test]** |

## Troubleshooting checklist {#troubleshooting}

1. Confirm **Remote Address**, **SSH Port**, and Linux user settings match your bastion settings.
1. Confirm your firewall allows the [!DNL Commerce Intelligence] IP addresses shown on your database credentials page.
1. Ask your infrastructure team whether SSH host keys on the bastion changed recently.
1. Run **[!UICONTROL Save & Test]** to validate settings and enroll keys if none exist yet.
1. Ask an Admin to run **[!UICONTROL Refresh SSH Host Keys]**, wait a few minutes, then run **[!UICONTROL Save & Test]** again. If the first refresh does not resolve the error, repeat this step.
1. If the connection still shows an SSH host key error after two refresh attempts, click **[!UICONTROL Contact Support]** on the connection page (or your account support channel).

## When to contact Adobe Support {#contact-support}

Contact support when:

* SSH host key errors continue after an Admin runs **[!UICONTROL Refresh SSH Host Keys]** twice and **[!UICONTROL Save & Test]** still fails
* **[!UICONTROL Refresh SSH Host Keys]** never completes or the connection status does not change after 15–30 minutes
* Errors began immediately after Adobe notified you of account migration or data server maintenance
* Bastion settings and firewall allowlisting are correct, your team has not rotated host keys, and you still cannot connect
* You need an Admin to run **[!UICONTROL Refresh SSH Host Keys]** but no Admin is available on the account

Include the connection name, approximate time of the last **[!UICONTROL Save & Test]** or refresh attempt, and whether bastion host keys changed recently. Do not send private keys or passphrases.

## Related {#related}

* [Connect MySQL via SSH tunnel](mysql-via-ssh-tunnel.md)
* [Connect MongoDB via SSH tunnel](mongodb-via-ssh-tunnel.md)
* [Connect PostgreSQL via SSH tunnel](postgresql.md)
* [Reauthenticating integrations](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
