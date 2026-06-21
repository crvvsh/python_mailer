# Python Mailer - Email Management Application

\![Status](https://img.shields.io/badge/status-active-brightgreen)
\![Python](https://img.shields.io/badge/python-3.9+-blue)
\![License](https://img.shields.io/badge/license-MIT-green)

## Overview

**Python Mailer** to aplikacja do zarządzania listami mailingowymi i wysyłania wiadomości email w skali. Projekt łączy backend w Pythonie z interfejsem web opartym na Flask, wspieranym przez GitHub Copilot Skills i Agents.

## Features

✅ **Subscriber Management** - Dodawanie, edytowanie, usuwanie subskrybentów  
✅ **Email Validation** - Zaawansowana walidacja adresów email  
✅ **Batch Sending** - Wysyłanie do wielu odbiorców  
✅ **Templates** - Szablony HTML i plain text  
✅ **Web Interface** - Intuicyjny interfejs Flask  
✅ **Error Handling** - Niezawodna obsługa błędów  
✅ **Logging** - Pełna historia wysyłanych wiadomości  

## Installation

### Requirements
- Python 3.9+
- pip / poetry
- Git

### Quick Start

```bash
# Clone repository
git clone https://github.com/crvvsh/python_mailer.git
cd python_mailer

# Create virtual environment
python3 -m venv venv
source venv/bin/activate

# Install dependencies
pip install -r requirements.txt

# Configure environment
cp .env.example .env
# Edit .env with your SMTP settings

# Run application
python web.py
```

Navigate to `http://localhost:5000`

## Project Structure

```
python_mailer/
├── mailer/
│   ├── email_sender.py       # Email sending logic
│   ├── subscribers.py        # Subscriber management
│   ├── validators.py         # Email validation
│   └── __init__.py
├── templates/
│   ├── base.html             # Base layout
│   ├── subscribers.html       # Subscriber list
│   ├── compose.html          # Compose email
│   └── history.html          # Send history
├── static/
│   ├── css/style.css         # Main stylesheet
│   └── js/app.js             # Frontend logic
├── tests/                    # Unit tests
├── web.py                    # Flask application
├── requirements.txt          # Python dependencies
└── copilot-instructions.md   # GitHub Copilot guidelines
```

## Usage

### 1. Add a Subscriber

```python
from mailer.subscribers import SubscriberManager

manager = SubscriberManager()
manager.add("user@example.com", "John Doe")
```

### 2. Validate Email

```python
from mailer.validators import EmailValidator

validator = EmailValidator()
is_valid = validator.validate("user@example.com")
print(is_valid)  # True/False
```

### 3. Send Email

```python
from mailer.email_sender import EmailSender

sender = EmailSender(
    smtp_host="smtp.gmail.com",
    smtp_port=587,
    username="your-email@gmail.com",
    password="your-app-password"
)

result = sender.send(
    to="user@example.com",
    subject="Hello\!",
    body="This is a test email."
)

print(result.success)  # True if sent
```

### 4. Web Interface

1. Open browser at `http://localhost:5000`
2. **Subscribers Tab** - View, add, remove subscribers
3. **Compose Tab** - Write and send emails
4. **History Tab** - View sent emails and status

## Configuration

### Environment Variables

Create `.env` file:

```env
# SMTP Settings
SMTP_HOST=smtp.gmail.com
SMTP_PORT=587
SMTP_USERNAME=your-email@gmail.com
SMTP_PASSWORD=your-app-password

# Flask Settings
FLASK_ENV=development
FLASK_DEBUG=True

# Database
DATABASE_URL=sqlite:///mailer.db
```

### SMTP Providers

#### Gmail
```
Host: smtp.gmail.com
Port: 587
Security: TLS
Password: Generate App Password in Google Account
```

#### Outlook
```
Host: smtp-mail.outlook.com
Port: 587
Security: TLS
```

#### Custom SMTP
```
Host: your-smtp-server.com
Port: 25/465/587
```

## API Reference

### Email Sender

```python
class EmailSender:
    def __init__(self, smtp_host, smtp_port, username, password)
    def send(to, subject, body, attachments=None)
    def send_batch(recipients, subject, body)
    def get_status(message_id)
```

### Subscriber Manager

```python
class SubscriberManager:
    def add(email, name, tags=None)
    def remove(email)
    def list_all()
    def list_by_tag(tag)
    def update(email, name, tags)
    def is_duplicate(email)
```

### Email Validator

```python
class EmailValidator:
    @staticmethod
    def validate(email)  # Returns True/False
    @staticmethod
    def validate_batch(emails)  # Returns dict
    @staticmethod
    def get_suggestions(invalid_email)  # Returns list
```

## Testing

Run tests with pytest:

```bash
# All tests
pytest

# With coverage
pytest --cov=mailer

# Specific test file
pytest tests/test_validators.py

# Verbose output
pytest -v
```

### Test Coverage Goals

- **Functions**: 100%
- **Branches**: 80%
- **Lines**: 85%

## GitHub Copilot Integration

Ten projekt jest skonfigurowany dla GitHub Copilot z następującymi komponentami:

### Instrukcje
- [`copilot-instructions.md`](copilot-instructions.md) - Globalne standardy projektu

### Skills
1. **email-validation** - Walidacja adresów email
2. **mailer-complete-testing** - Framework testowania
3. **email-templates** - Projektowanie szablonów

### Agents
- **Documentation Generator** - Automatyczne generowanie dokumentacji

## Common Tasks

### Add Multiple Subscribers from CSV

```python
import csv
from mailer.subscribers import SubscriberManager

manager = SubscriberManager()

with open('subscribers.csv', 'r') as f:
    reader = csv.DictReader(f)
    for row in reader:
        manager.add(row['email'], row['name'], row['tags'])
```

### Send Newsletter Template

```python
from mailer.email_sender import EmailSender
from jinja2 import Template

sender = EmailSender(...)
subscribers = manager.list_all()

template = Template(open('newsletter.html').read())

for sub in subscribers:
    body = template.render(name=sub['name'])
    sender.send(sub['email'], "Newsletter", body)
```

### Export Send History

```python
import json
from mailer.email_sender import EmailSender

sender = EmailSender(...)
history = sender.get_history()

with open('history.json', 'w') as f:
    json.dump(history, f, indent=2)
```

## Troubleshooting

### "SMTP Connection Failed"
- Check your SMTP credentials
- Verify port number (usually 587 for TLS, 465 for SSL)
- Check firewall/network restrictions
- Enable "Less Secure Apps" (Gmail)

### "Invalid Email Address"
- Check RFC 5322 compliance
- Remove extra spaces
- Verify domain extension (.com, .org, etc.)

### "Database Locked"
- Close other connections
- Delete `mailer.db` and restart
- Use PostgreSQL for production

### "Missing Dependencies"
```bash
pip install --upgrade pip
pip install -r requirements.txt
```

## Performance Tips

1. **Batch Sending** - Use `send_batch()` instead of loop
2. **Connection Pooling** - Reuse SMTP connections
3. **Async Processing** - Use Celery for large campaigns
4. **Caching** - Cache subscriber lists

## Security

⚠️ **Important Security Notes:**

- **Never commit credentials** - Use `.env` files
- **Validate all inputs** - Filter email addresses, subject lines
- **Use TLS/SSL** - Always encrypt SMTP connection
- **Implement Rate Limiting** - Prevent abuse
- **Monitor Bounce Rates** - Maintain sender reputation
- **GDPR Compliance** - Implement unsubscribe mechanism

## Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit changes (`git commit -m 'feat: Add amazing feature'`)
4. Push to branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

See [`copilot-instructions.md`](copilot-instructions.md) for coding standards.

## Changelog

### v1.0.0 (2026-06-21)
- ✨ Initial release
- ✅ Basic subscriber management
- ✅ Email validation
- ✅ Flask web interface
- ✅ GitHub Copilot integration

## FAQ

**Q: Can I use this for commercial purposes?**  
A: Yes, it's MIT licensed.

**Q: How many subscribers can I manage?**  
A: Depends on database, but tested up to 100k.

**Q: Does it support HTML emails?**  
A: Yes, both HTML and plain text.

**Q: Can I schedule emails?**  
A: Not yet, but planned for v2.0.

**Q: Is there a mobile app?**  
A: Currently web-only, mobile planned.

## Support

- 📧 Email: support@example.com
- 💬 Issues: GitHub Issues
- 📚 Docs: [Full Documentation](https://github.com/crvvsh/python_mailer/wiki)
- 🐦 Twitter: [@python_mailer](https://twitter.com/python_mailer)

## License

This project is licensed under the MIT License - see [LICENSE](LICENSE) file for details.

## Acknowledgments

- Built with ❤️ using Python & Flask
- Powered by GitHub Copilot
- Inspired by Mailchimp, SendGrid

---

**Made with 🚀 by Python Mailer Community**
