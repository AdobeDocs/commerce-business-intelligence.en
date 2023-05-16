---
title: Restricting Access to your Database
description: Learn how you can restrict access, limiting access to the server that houses your database.
exl-id: 7a0bc0d7-086e-4a6e-b1dd-6db13814710e
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

Once this is complete, the user you created for [!DNL Commerce Intelligence] cannot make changes to your system.
