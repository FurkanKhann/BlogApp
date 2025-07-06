# 📰 NewsAI — Fake News Detection App

NewsAI is a Flask-based web application where users can register, create posts, like, report, and verify news using Google's **Gemini AI model**. The platform incorporates a Gemini-powered fact-checking system to detect potential misinformation in user-submitted posts.

## 🚀 Live Demo

🔗 [https://blogapp-production-4765.up.railway.app/home]()  


---

## 📂 Project Structure
```
C:.
│   .env
│   gem.py
│   render.yaml
│   requirements.txt
│   run.py
│   text.py
│   
├───flaskblog
│   │   forms.py
│   │   models.py
│   │   routes.py
│   │   __init__.py
│   │   
│   ├───static
│   │   │   main.css
│   │   │
│   │   └───profile_pic
│   │
│   ├───templates
│   │       about.html
│   │       account.html
│   │       create_post.html
│   │       home.html
│   │       layout.html
│   │       login.html
│   │       post.html
│   │       register.html
│   │       reset_request.html
│   │       reset_token.html
│   │       user_posts.html
│   │
│   └───__pycache__
│           form.cpython-313.pyc
│           forms.cpython-313.pyc
│           models.cpython-313.pyc
│           routes.cpython-313.pyc
│           __init__.cpython-313.pyc
│
└───instance
        site.db
```

---

## 💡 Features

- 🧾 **User Authentication**
  - Register/Login/Logout
  - Password Reset via Email
- 📝 **Blog Posting**
  - Create, update, and delete posts
  - Like or report others' posts
- 🤖 **Fake News Detection**
  - Automatically checks posts via **Gemini AI**
  - Flags suspicious content using AI-generated verdict
- 📸 **User Profiles**
  - Upload and manage profile pictures
- 📊 **Post Insights**
  - Likes vs Reports shown clearly
- 🌐 **Responsive UI** with custom CSS and Bootstrap

---

## 🛠️ Tech Stack

- **Python 3.x**
- **Flask**
- **Flask-WTF**, **Flask-Login**, **Flask-Mail**, **Flask-Bcrypt**
- **SQLite (SQLAlchemy)**
- **Google Generative AI (`gemini-2.5-flash`)**
- **Pillow** for image handling
- **Deployed on [Railway](https://railway.app)** or **Render**

---

## ⚙️ Setup Instructions

### 1. Clone the repository

```bash
git clone https://github.com/FurkanKhann/BlogApp.git
cd NewsAI
```

### 2. Create a virtual environment and install dependencies
``` bash
python -m venv venv
source venv/bin/activate  # For Windows: venv\Scripts\activate
pip install -r requirements.txt
```
### 3. Create .env file
``` bash
SECRET_KEY=your_secret_key
EMAIL_USER=youremail@example.com
EMAIL_PASS=your_email_password
API_KEY=your_google_gemini_api_key
```
### 4. Run the app
``` bash
python run.py
```
## 🚀 Deployment (Railway/Render)
1. Ensure you have a render.yaml file for Render or configure Railway environment variables.
2. Add this to your root:
``` bash
Procfile
------
web: gunicorn run:app
```
3. Push to GitHub and connect your repo to Render or Railway.
4. Set all environment variables (.env) on the platform dashboard.
   


