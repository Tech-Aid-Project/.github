# 🏛️ Tech Aid – Software Architecture

**Tech Aid** is an educational platform focused on **digital inclusion** with a focus on accessibility and gamification. This architecture adopts the **microservices** style to ensure modularity, scalability and independence between components.

---

## 🗂️ Project Structure


# 🏛️ Suggested Architecture
```
tech-aid/
├── auth-service/
├── user-profile-service/
├── content-service/
├── gamification-service/
├── notification-service/
├── front-end/
└── docker-compose.yml
```
```
[User]
 ↓
[Frontend (React)]
 ↓
[API Gateway]
 ┌────────────┬────────────── ┬────────────┬──────────────┐
 ↓ ↓ ↓ ↓ ↓
Auth User Profile Content Gamification Notifications
Service Service Service Service Service
```

## 🔧 Microservices

### `1. auth-service`
- **Responsible for**: Registration, login, authentication with JWT.
- **Stack**: Node.js + Express + PostgreSQL + bcrypt + JWT.
- **Endpoints**:
- `POST /register`
- `POST /login`
- `GET /verify-token`

---

### `2. user-profile-service`
- **Responsible for**: Storing and managing user profiles.
- **Stack**: Python (FastAPI) + MongoDB.
- **User fields**: name, age, email, preferences, progress, accessibility settings.
- **Endpoints**:
- `GET /users/:id`
- `PUT /users/:id`
- `GET /users/:id/progress`

---

### `3. content-service`
- **Responsible for**: CRUD of lessons, videos, quizzes and materials.
- **Stack**: Node.js + Express + MongoDB.
- **Admin panel**: Optional, can be done with React Admin or Strapi.
- **Endpoints**:
- `GET /lessons`
- `POST /lessons`
- `PUT /lessons/:id`
- `DELETE /lessons/:id`

---

### `4. gamification-service`
- **Responsible for**: Points rules, progress, badges and achievements.
- **Stack**: Python + Redis (cache) + PostgreSQL (persistence). - **Examples of achievements**:
- "First Login"
- "Completed 5 lessons"
- "Logged in 7 days in a row"
- **Endpoints**:
- `GET /user/:id/badges`
- `POST /user/:id/complete-lesson`

---

### `5. notification-service` (optional)
- **Responsible for**: Sending emails and messages (e.g. WhatsApp, SMS).
- **Stack**: Python + Celery + Redis + SendGrid/Twilio.
- **Usage**: Scheduling reminders, congratulations, lesson confirmations.
- **Task queue**: Asynchronous with Celery.

---
### `6. front-end`
- **Stack**: React (with Vite or CRA) + Tailwind CSS + Axios. - **Function**: Consumes APIs from microservices and displays the interface to the user.
- **Highlights**:
- Modern componentization
- Accessibility support (ARIA, large font, high contrast)
- React Router for navigation
- Context API or Zustand for global state
## 🛢️ Database

| Service | Database | Rationale |
|------------------------|--------------------|--------------------------------------------------|
| `auth-service` | PostgreSQL | Critical data consistency and integrity |
| `user-profile-service` | MongoDB | Flexibility for user preferences |
| `content-service` | MongoDB | Dynamic framework for educational content |
| `gamification-service` | Redis + PostgreSQL | Cache for speed + achievement persistence |
| `notification-service` | Redis + PostgreSQL | Queue + log of sent notifications |

---

## 📦 Orchestration (Docker)

The `docker-compose.yml` centralizes all services:
- Each microservice in its container.
- Database coupled to each service.
- HTTP communication between services.

---
## ☁️ Hosting

| Component | Recommended service |
|------------|--------------------------|
| Front-end | Vercel / Netlify |
| Back-end | Railway / Render / Fly.io|
| DB | MongoDB Atlas / Supabase|

---
## 🎮 Gamification

- Achievements unlocked based on actions (e.g. completing a class).
- Progress bar and level system.
- Simple and stimulating visual rewards.

---
## ♿ Accessibility

- High contrast buttons.
- Large and legible font.
- Smooth animations.
- Compatibility with screen readers.
- Simple navigation with visual and textual feedback.
- Night mode

---

## ✅ Conclusion

This architecture was designed to be **modular, scalable, accessible and educational**, respecting the principles of digital inclusion and good software engineering practices.

> Tech Aid is not just technology — it is a step towards bringing generations together with empathy and innovation.
