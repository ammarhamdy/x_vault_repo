
# Installation
```sh
sudo apt install sendemail
```

# Basic Syntax
```sh
sendemail -f FROM -t TO -u SUBJECT -m MESSAGE -s SMTP_SERVER[:PORT] [options]
```

## Required flags:
- `-f` → From address (the sender)
- `-t` → To address (the recipient)
- `-u` → Subject
- `-m` → Message body
- `-s` → SMTP server and port (e.g., `smtp.gmail.com:587`)

## Optional (but usually needed)
- `-xu` → SMTP username (login)
- `-xp` → SMTP password (or Gmail App Password if using Gmail)
- `-o tls=yes` → Enable TLS (for secure SMTP)

# Use gmail
If you want to send through Gmail:
```sh
sendemail \
  -f "yourname@gmail.com" \
  -t "recipient@example.com" \
  -u "Test Subject" \
  -m "This is the body of the email." \
  -s smtp.gmail.com:587 \
  -xu "yourname@gmail.com" \
  -xp "YOUR_APP_PASSWORD" \
  -o tls=yes
```
- You must use an **App Password** (Google blocks normal account passwords).
- Set up in Google Account → Security → App passwords.

