---
title: Restricting Access to your Database
description: Learn how you can restrict access, limiting access to the server that houses your database.
exl-id: 7a0bc0d7-086e-4a6e-b1dd-6db13814710e
role: Admin, User
feature: Accounts, User Management
TQID: https://experienceleague.adobe.com/O2cS-hbhjqktc4LpJD6agxgIwabrypgCY9fnJTCR2XM
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
    internal-label: Commerce Intelligence
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
    internal-label: Accounts
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
---
# Restrict Access

When you create an SSH tunnel to your server, there is no need for [!DNL Adobe Commerce Intelligence] to have access to anything but the database. If you do not want [!DNL Commerce Intelligence] to have full access to the server that houses your database, you can restrict access by forcing the [!DNL Commerce Intelligence Linux] user into a [restricted bash shell](https://www.gnu.org/software/bash/manual/html_node/The-Restricted-Shell.html).

You may have guessed from the name, but a restricted bash shell is used to set up an environment more controlled than the standard shell. The important thing about this type of shell is that restricted shell users cannot access system functions or make any kind of modifications.

To restrict the [!DNL Commerce Intelligence Linux] user, you must do two things:

1. Change the PATH environment variable to be the empty string. This means that the user cannot access system executables.

1. Make sure that the shell executed is `bash -r`

Both of these can be done inside the `authorized_keys` file in the user's home `dir/.ssh` directory as part of the command that is executed when the user logs in. It looks something like this:

```bash
... other keys ...
command="env PATH="" /bin/bash -r" <rjmetrics public key goes here>
... other keys ...
```

When this is complete, the user you created for [!DNL Commerce Intelligence] cannot make changes to your system.
