# 🎯 NewsAI (BlogApp) — Interview Preparation Guide

This document contains a project overview, technical details, and potential interview questions and answers to help you prepare for technical interviews.

---

## 1. 📊 Project Overview (The Elevator Pitch)

**"NewsAI is a full-stack Flask web application that serves as a social platform for news sharing, with a twist: it uses Google's Gemini AI to automatically fact-check user-submitted posts. Users can register, post news, like, and report content. Before a post is displayed, the Gemini API analyzes the content to detect potential misinformation."**

**Core Tech Stack:**
* **Backend:** Python, Flask, SQLAlchemy (ORM)
* **Frontend:** HTML/CSS (Jinja2 Templates), Bootstrap
* **AI Integration:** Google Generative AI (Gemini 2.5 Flash)
* **Authentication:** Flask-Login, Flask-Bcrypt
* **Deployment:** Render

---

## 2. 🏛️ Architecture & Database Design

### Database Models (`models.py`)
The application uses a relational database (SQLite for dev, Postgres for prod) with the following core models:
* **User:** `id`, `username`, `email`, `image_file`, `password`, `posts` (Relationship).
* **Post:** `id`, `title`, `date_posted`, `content`, `user_id` (Foreign Key).
* **Association Tables (Many-to-Many):**
  * `likes`: Links `user_id` and `post_id`.
  * `reports`: Links `user_id` and `post_id`.

### AI Integration (`gem.py`)
* The app uses the `google-generativeai` SDK.
* It passes the post content to Gemini with a strict system prompt: *"Given the following post content, respond with only `true` if the news seems likely to be true, or `false` if it seems fake."*
* This acts as an automated content moderation system.

---

## 3. 💬 Common Interview Questions & Answers

### Q1: How does the AI fact-checking feature work in your application?
**A:** "When a user submits a news post, the backend intercepts the content before saving it to the database (or before displaying it as verified). I use the `google.generativeai` library to send the content to the Gemini 2.5 Flash model. I designed a strict prompt instructing the AI to act as a fact-checker and return a boolean-like string (`true` or `false`) based on whether the news seems authentic or fake. This result is then used to flag or verify the post."

### Q2: How did you implement user authentication and security?
**A:** "I used `Flask-Login` for session management, which handles logging users in and out and protecting routes via the `@login_required` decorator. For security, passwords are never stored in plain text; I used `Flask-Bcrypt` to hash passwords before storing them in the database. I also implemented a secure password reset flow using `itsdangerous` to generate time-sensitive tokens sent via email (`Flask-Mail`)."

### Q3: What is SQLAlchemy and why did you use it?
**A:** "SQLAlchemy is an Object-Relational Mapper (ORM) for Python. I used it because it allows me to interact with the database using Python classes instead of writing raw SQL queries. It handles SQL injection prevention automatically and makes it very easy to switch databases (e.g., from SQLite in development to PostgreSQL in production) without changing the codebase."

### Q4: Explain the many-to-many relationship in your app (Likes/Reports).
**A:** "A user can like multiple posts, and a post can be liked by multiple users. To handle this in SQLAlchemy, I created an association table called `likes` containing two foreign keys: `user_id` and `post_id`. I did the same for the `reports` feature. This allows me to easily query how many likes a post has, or check if a specific user has already liked a specific post."

### Q5: What was a major challenge you faced and how did you solve it?
**A:** *(Choose one that sounds best)*
* **Challenge (AI Prompt Engineering):** "Initially, the Gemini AI was returning long explanations instead of a simple boolean verification. I had to refine the prompt engineering to strictly output `true` or `false` without extra characters, ensuring the backend could programmatically parse the response."
* **Challenge (Routing/State):** "Handling pagination alongside likes and reports was tricky. I had to ensure that when a user clicks 'Like', the page doesn't just reload to the top, but maintains the state and current pagination page."

### Q6: How are environment variables managed in this project?
**A:** "Sensitive information like the `SECRET_KEY`, Database URIs, Email credentials, and the `API_KEY` for Gemini are stored in a `.env` file. I used the `python-dotenv` package to load these variables into the Flask app configuration. The `.env` file is added to `.gitignore` so secrets are never pushed to GitHub."

---

## 4. 🚀 Future Improvements (If asked "What would you add next?")
* **Caching:** Use Redis to cache the AI verification results so we don't query the Gemini API for the exact same news post multiple times.
* **WebSockets:** Add real-time notifications for when a user's post gets liked or reported.
* **Admin Dashboard:** Create a role-based access control (RBAC) system where an Admin can review posts that have been flagged as 'false' by the AI.
