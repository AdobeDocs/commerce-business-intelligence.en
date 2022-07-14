---
title: Restricting access to your database
zendesk_id: 360016732111
---

When we create an SSH tunnel to your server, there's no need for Magento BI to have access to anything but the database. If you don't want Magento BI to have full access to the server that houses your database, you can restrict access by forcing the Magento BI Linux user into a [restricted bash shell](https://www.gnu.org/software/bash/manual/html_node/The-Restricted-Shell.html).

You may have guessed from the name, but a restricted bash shell is used to set up an environment more controlled than the standard shell. The important thing about this type of shell is that restricted shell users can't access system functions or make any kind of modifications.

To restrict the Magento BI Linux user, you'll need to do two things:

1. Change the PATH environment variable to be the empty string. This means the user won't be able to access system executables.
1. Make sure that the shell executed is `bash -r`

Both of these can be done inside the 'authorized_keys' file in the user's home dir/.ssh directory as part of the command that is executed when the user logs in. It will look something like this:

```bash
... other keys ...
command="env PATH="" /bin/bash -r" <rjmetrics public key goes here>
... other keys ...
```

Once this is complete, the user you created for Magento BI won't have the ability to make any changes to your system.
