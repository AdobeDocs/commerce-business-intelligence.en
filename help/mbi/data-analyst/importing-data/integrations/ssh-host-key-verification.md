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

This model improves security by blocking man-in-the-middle and unexpected host changes. It also means that host key rotation, missing trust material, or infrastructure changes can surface as SSH host key errors on the connection instead of generic tunnel failures. If your team rotates bastion host keys or the bastion identity changes, an Admin must run **[!UICONTROL Refresh SSH Host Keys]**. Saving the connection again does not update enrolled keys by itself.

>[!NOTE]
>
>Only Admin users can run **[!UICONTROL Refresh SSH Host Keys]**. If you do not see this control, ask an Admin on your account to run the refresh or contact Adobe Support.

## Expected behavior for Save & Test {#save-and-test}

**[!UICONTROL Save & Test]** performs **initial SSH host key enrollment only**. It is conservative by design and does not rotate or overwrite keys that are already enrolled for the connection.

>[!IMPORTANT]
>
>Host key rotation requires an Admin to run **[!UICONTROL Refresh SSH Host Keys]**. If bastion host keys changed or the bastion identity changed (hostname, IP, or port), running **[!UICONTROL Save & Test]** again or re-saving the connection does not update enrolled keys. The connection can keep failing until an Admin refreshes host keys.

| Enrolled host key state | What Save & Test does |
| --- | --- |
| Host keys not yet enrolled | Scans the bastion host and port, enrolls the host keys, and stores them for this connection |
| Host keys already enrolled | Skips enrollment. Does not overwrite, rotate, or delete existing enrolled keys, even if live bastion keys no longer match |
| Enrolled keys missing, empty, or invalid | Does not repair invalid trust material by itself. Use **[!UICONTROL Refresh SSH Host Keys]** or contact Support if errors continue |

After a successful first enrollment, later **[!UICONTROL Save & Test]** runs validate credentials and connection settings but leave enrolled SSH host keys unchanged. Use **[!UICONTROL Refresh SSH Host Keys]** when bastion host keys rotate or the bastion identity changes.

## Expected behavior for Refresh SSH Host Keys {#refresh-ssh-host-keys}

**[!UICONTROL Refresh SSH Host Keys]** updates enrolled SSH host keys when the bastion has changed or when trust material must be repaired. An Admin starts the refresh from the connection in **[!UICONTROL Data]** > **[!UICONTROL Connections]**.

The refresh runs asynchronously on Adobe infrastructure assigned to your account. The Admin UI returns after the job is queued. It does not run the scan on your workstation.

A refresh **rewrites** enrolled host keys only when one of these conditions is true:

* Enrolled host keys are missing
* The enrolled file is empty
* Enrolled host keys cannot be read
* Enrolled host keys fail validation
* A new scan returns different host key lines than the enrolled file
* Fingerprints from the scan and enrolled file do not match

If enrolled keys are current and valid, the refresh completes without changing them.

>[!TIP]
>
>Run **[!UICONTROL Refresh SSH Host Keys]** after your team rotates SSH host keys on the bastion, changes the bastion hostname or IP, or replaces the SSH endpoint. Wait a few minutes, then run **[!UICONTROL Save & Test]** to confirm the connection.

## Expected behavior during account migration {#migration}

Adobe may move your [!DNL Commerce Intelligence] account between data servers during maintenance or scaling. Enrolled SSH host keys are copied to the destination so strict verification continues to work after the move.

| Situation | Expected result |
| --- | --- |
| Host keys already enrolled in the current layout | Keys are copied to the destination. **[!UICONTROL Save & Test]** skips re-enrollment and does not overwrite them |
| Only legacy enrolled key storage exists on the source | Keys are migrated into the current per-connection layout on the destination |
| After migration completes | Run **[!UICONTROL Save & Test]**. Enrollment should be skipped if keys were copied successfully |
| Host keys still fail after migration | An Admin should run **[!UICONTROL Refresh SSH Host Keys]** to repair missing or invalid trust material |

You do not manage enrolled host key files directly. Adobe Support handles migration issues that persist after **[!UICONTROL Save & Test]** and **[!UICONTROL Refresh SSH Host Keys]**.

## SSH host key error messages {#ssh-host-key-errors}

Connection status shows a single user-friendly SSH host key message. Raw OpenSSH errors are not shown in the dashboard.

The following table maps common messages to likely causes and customer actions.

| Message or status | What it means | Possible causes | What you should do |
| --- | --- | --- | --- |
| SSH host key verification failed | The bastion host key does not match enrolled keys, or trust material is unusable | SSH host keys rotated on the bastion; bastion hostname, IP, or port changed; enrolled keys missing, empty, invalid, or unreadable | Confirm **Remote Address** and **SSH Port** on the connection. Ask your infrastructure team whether bastion host keys changed. An Admin runs **[!UICONTROL Refresh SSH Host Keys]**, waits a few minutes, then runs **[!UICONTROL Save & Test]** |
| SSH host keys could not be enrolled | **[!UICONTROL Save & Test]** could not scan or store bastion host keys | Bastion unreachable from Adobe infrastructure; DNS failure; firewall blocks [!DNL Commerce Intelligence] IP addresses; wrong **Remote Address** or **SSH Port**; `ssh-keyscan` failure on the bastion | Verify that your firewall allows the [!DNL Commerce Intelligence] IP addresses on the database credentials page. Confirm the bastion is up and accepts SSH on the configured port. Correct connection fields and run **[!UICONTROL Save & Test]** again |
| SSH host keys are missing or invalid | Strict verification blocked the tunnel because enrolled trust material is absent or corrupt | First connection never completed enrollment; prior refresh failed; migration did not copy keys; filesystem or permission issue on Adobe infrastructure | An Admin runs **[!UICONTROL Refresh SSH Host Keys]**, then **[!UICONTROL Save & Test]**. If the error persists, contact Support |
| Refresh SSH host keys could not be completed | The refresh job did not update enrolled keys | Replication worker not processing jobs; network, DNS, or scan failure during refresh; permission issue on Adobe infrastructure | Wait several minutes and run **[!UICONTROL Refresh SSH Host Keys]** again. Confirm bastion reachability and allowlisting. Contact Support if the connection still fails after two refresh attempts |

## Troubleshooting checklist {#troubleshooting}

1. Confirm **Remote Address**, **SSH Port**, and Linux user settings match your bastion.
1. Confirm your firewall allows the [!DNL Commerce Intelligence] IP addresses shown on your database credentials page.
1. Ask your infrastructure team whether SSH host keys on the bastion changed recently.
1. Run **[!UICONTROL Save & Test]** to validate settings and enroll keys if none exist yet.
1. Ask an Admin to run **[!UICONTROL Refresh SSH Host Keys]**, wait a few minutes, then run **[!UICONTROL Save & Test]** again.
1. If the connection still shows an SSH host key error, use **[!UICONTROL Contact Support]** on the connection page (or your account support channel).

## When to contact Adobe Support {#contact-support}

Contact Support when:

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
