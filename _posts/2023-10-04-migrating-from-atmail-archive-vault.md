This document provides a description on how to migrate from atmail's archivevault to piler.

### Importing emails from archivevault

Atmail archivevault stores emails under /usr/local/archivevault/messages in bzip2 compressed files. Even though archivevault doesn't offer an export tool, the process is pretty straightforward. Atmail does not use deduplication, so each bz2 file represents an email.

Run the following commands to import emails:

```
cd /tmp
for i in `find /usr/local/archivevault/messages -name \*.bz2`; do bzip2 -dc | pilerimport -e - ; done
```

When the process is done, you have your emails in piler. If you decided to use another host for piler, then you should either NFS mount archivevault's directory to the piler host or copy the emails with rsync or scp, etc to the piler host before importing.
