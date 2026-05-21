# Flask Job Application Form

A Flask web application that allows users to submit a job application form. Submissions are saved to a SQLite database and an automated confirmation email is sent to the applicant via Gmail.

---

## Features

- Job application form with first name, last name, email, availability date, and current occupation
- Form submissions saved to a SQLite database using SQLAlchemy
- Automated confirmation email sent to the applicant on successful submission
- Flash message confirmation displayed in the browser after submission
- Environment variables used to keep email credentials secure
- Responsive UI built with Bootstrap 5

---

## Project Structure

```
Flask_form_APP/
│
├── main.py                  # Flask app, database model, route logic, email
├── templates/
│   └── index.html           # Job application form (Bootstrap 5)
├── instance/
│   └── database.db          # SQLite database (auto-created on first run)
├── .env                     # Email credentials — NOT committed to GitHub
├── .gitignore               # Excludes .env and database from version control
└── README.md
```

---

## Requirements

- Python 3.13+
- A Gmail account with an [App Password](https://support.google.com/accounts/answer/185833) configured

Install dependencies:

```bash
pip install flask flask-sqlalchemy flask-mail python-dotenv
```

---

## Setup

1. Clone the repository:

```bash
git clone https://github.com/your-username/Flask_form_APP.git
cd Flask_form_APP
```

2. Create and activate a virtual environment:

```bash
python -m venv .venv
source .venv/bin/activate       # macOS/Linux
.venv\Scripts\activate          # Windows
```

3. Install dependencies:

```bash
pip install flask flask-sqlalchemy flask-mail python-dotenv
```

4. Create a `.env` file in the project root with your Gmail credentials:

```
MAIL_USERNAME=your_email@gmail.com
MAIL_PASSWORD=your_gmail_app_password
```

> **Important:** Never commit your `.env` file to GitHub. Make sure it is listed in your `.gitignore`.

5. Run the app:

```bash
python main.py
```

6. Open your browser and go to `http://127.0.0.1:5001`

---

## Gmail App Password Setup

This app uses Gmail's SMTP server. Google requires an **App Password** rather than your regular account password when using SMTP:

1. Go to your Google Account → Security
2. Enable 2-Step Verification if not already active
3. Go to Security → App Passwords
4. Generate a new App Password for "Mail"
5. Use that 16-character password as `MAIL_PASSWORD` in your `.env` file

---

## How It Works

### `main.py`

| Component | Description |
|---|---|
| `load_dotenv()` | Loads email credentials from `.env` |
| `app.config` | Configures Flask, SQLAlchemy, and Flask-Mail |
| `Form` model | SQLAlchemy model storing each submission in `database.db` |
| `index()` route | Handles GET (render form) and POST (save to DB, send email, flash message) |
| `db.create_all()` | Creates the database table on first run |

### `index.html`

Bootstrap 5 form with fields for first name, last name, email, availability date, and occupation (radio buttons). Displays a success flash message after submission.

---

## .gitignore

Make sure your `.gitignore` includes the following to avoid exposing credentials or committing unnecessary files:

```
.env
instance/
__pycache__/
.venv/
*.pyc
```

---

## Troubleshooting

| Problem | Likely cause | Fix |
|---|---|---|
| `KeyError: MAIL_USERNAME` | Quotes missing around config key | Use `app.config["MAIL_USERNAME"]` not `app.config[MAIL_USERNAME]` |
| Email not sending | Gmail App Password not set up | Follow the Gmail App Password steps above |
| `SMTPAuthenticationError` | Wrong password in `.env` | Double-check your App Password in `.env` |
| Database not created | `db.create_all()` not called | Ensure it runs inside `with app.app_context()` before `app.run()` |
| Form submits but no flash message | Flash not rendering in template | Check `get_flashed_messages()` block is present in `index.html` |

---

## Built With

- [Flask](https://flask.palletsprojects.com/) — web framework
- [Flask-SQLAlchemy](https://flask-sqlalchemy.palletsprojects.com/) — database ORM
- [Flask-Mail](https://pythonhosted.org/Flask-Mail/) — email sending
- [python-dotenv](https://pypi.org/project/python-dotenv/) — environment variable management
- [Bootstrap 5](https://getbootstrap.com/) — frontend styling

---

## License

MIT License

Copyright (c) 2026 Peter Thomson

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

---

## Disclaimer

This project is intended for educational and demonstration purposes only. It is
not intended for use in a production environment without appropriate security
hardening, including but not limited to: replacing the development secret key,
using a production-grade WSGI server, and securing all credentials. The author
accepts no responsibility for any misuse or damage arising from the use of this
software.

---

*Author: Peter Thomson*
*Last updated: 21/05/2026*