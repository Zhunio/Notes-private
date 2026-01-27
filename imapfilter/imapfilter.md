# iMapFilter

## 1. Install imapfilter

```bash
brew install imapfilter
```

## 2. Create imapfiler config

```lua
-- ~/.config/imapfilter/config.lua
options.timeout = 120
options.subscribe = true

icloud = IMAP({
	server = "imap.mail.me.com",
	username = "<email>",
	password = "<password>",
	ssl = "tls1",
})

inbox = icloud["INBOX"]

-- Move GitHub emails
github = inbox:contain_from("github.com")
github:move_messages(icloud["GitHub"])

kohls = inbox:contain_from("kohls.com")
kohls:move_messages(icloud["Junk"])

```

## 3. Setup cron job

Create imapfilter log

```bash
touch ~/.config/imapfilter/logs/imapfilter.log
```

Edit your crontab file

```bash
crontab -e
```

This cron job runs imapfilter every 5 minutes and appends the output to the log file.

```bash
*/5 * * * * /usr/local/bin/imapfilter -c /Users/<user>/.config/imapfilter/config.lua >> /Users/<user>/.imapfilter/logs/imapfilter.log 2>&1
```

> [NOTE]
> <user> username on your macOS
> <email> imap email
> <password> imap password
