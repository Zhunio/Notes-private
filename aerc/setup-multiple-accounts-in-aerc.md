# Setup for multiple email accounts in aerc

```sh
brew install aerc oauth2l
```

## Configuration

- `<email>`: Your email address (e.g. example@icloud.com)
- `<pass>`: Your app-specific password for iCloud email
- `<fullName>`: Your full name (e.g. John Doe)
- `~/.oauth/mail.work.json`: OAuth 2.0 credentials file from Google Cloud Console
- `~/.oath2l`: Cache file for oauth2l tokens (will be created automatically by oauth2l)

```conf
# ~/.config/aerc/accounts.conf
[icloud]
source            = imaps://<email>:<pass>@imap.mail.me.com:993
outgoing          = smtp://<email>:<pass>@smtp.mail.me.com:587
from              = <fullName> <email>
default           = INBOX
copy-to           = Sent Messages
cache-headers     = true
folders-sort      = INBOX,Sent Messages,Archive,Trash,Junk

[gmail]
source            = imaps+xoauth2://<email>@imap.gmail.com:993
outgoing          = smtp+xoauth2://<email>@smtp.gmail.com:587
from              = <fullName> <email>
source-cred-cmd   = ~/.get-token.sh
outgoing-cred-cmd = ~/.get-token.sh
folder-map        = ~/.config/aerc/folder-map.conf
folders-sort      = INBOX,Important,Sent Mail,Drafts,Starred,Trash
folders-exclude   = All Mail
default           = INBOX
copy-to           = Sent Mail
cache-headers     = true
```

```sh
# ~/.get-token.sh
oauth2l fetch \
--credentials ~/.oauth/mail.work.json \
--scope https://mail.google.com \
--cache ~/.oauth2l \
--refresh
```
