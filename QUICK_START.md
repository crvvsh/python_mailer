# 🚀 Python Mailer - Quick Start Guide

## 5-Minute Setup

### 1️⃣ Clone & Setup (1 min)
```bash
git clone https://github.com/crvvsh/python_mailer.git
cd python_mailer
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```

### 2️⃣ Configure SMTP (2 min)
```bash
cp .env.example .env
# Edit .env with your email provider settings
```

**Gmail Example:**
```
SMTP_HOST=smtp.gmail.com
SMTP_PORT=587
SMTP_USERNAME=your-email@gmail.com
SMTP_PASSWORD=your-app-password  # From Google App Passwords
```

### 3️⃣ Run Application (1 min)
```bash
python web.py
```

Then open: **http://localhost:5000** 🎉

---

## First Steps

### Add Your First Subscriber
1. Click "Subscribers" tab
2. Enter email and name
3. Click "Add"

### Send Your First Email
1. Click "Compose" tab
2. Select recipient
3. Write subject & message
4. Click "Send"

---

## Python API Usage

### Import & Initialize
```python
from mailer.email_sender import EmailSender
from mailer.subscribers import SubscriberManager

manager = SubscriberManager()
sender = EmailSender(
    smtp_host="smtp.gmail.com",
    smtp_port=587,
    username="your-email@gmail.com",
    password="your-app-password"
)
```

### Add Subscriber
```python
manager.add("user@example.com", "John Doe")
```

### Validate Email
```python
from mailer.validators import EmailValidator
validator = EmailValidator()
print(validator.validate("user@example.com"))  # True
```

### Send Email
```python
result = sender.send(
    to="user@example.com",
    subject="Hello\!",
    body="Welcome to Python Mailer"
)
print(f"Sent: {result.success}")
```

### Send to Multiple Recipients
```python
subscribers = manager.list_all()
for sub in subscribers:
    sender.send(
        to=sub['email'],
        subject="Newsletter",
        body="Latest updates..."
    )
```

---

## Common Issues & Solutions

| Issue | Solution |
|-------|----------|
| SMTP Connection Failed | Check credentials and port in .env |
| "Invalid Email Address" | Verify email format (user@domain.com) |
| Database Locked | Delete mailer.db and restart |
| Module Not Found | Run `pip install -r requirements.txt` |

---

## Next Steps

📚 **Read Full Documentation**: Open `README.md`  
🌐 **Interactive Guide**: Open `GETTING_STARTED.html` in browser  
🔗 **GitHub**: https://github.com/crvvsh/python_mailer  
💡 **Ideas**: Check GitHub Issues for feature requests  

---

## Support

- 📧 Problems? Create an [Issue](https://github.com/crvvsh/python_mailer/issues)
- 📖 Questions? Check [FAQ in GETTING_STARTED.html](GETTING_STARTED.html)
- 🚀 Want to help? [Contributions welcome\!](README.md#contributing)

**Happy mailing\! 📨**
