# amber-wisteria

Repository for Team Amber Wisteria - Spring 2026 Cohort

## How to contribute

1. Clone the repository  
   `git clone https://github.com/nhcarrigan-spring-2026-cohort/amber-wisteria.git`

2. Create a new branch based on your task or issue:  
   `git checkout -b feature/your-name-task`

3. Make your changes and commit them clearly:  
   `git commit -m "Add: login form component"`

4. Push your branch:  
   `git push origin feature/your-name-task`

5. Open a pull request to `main` using this template:

```
- Summary
What changed?

- Linked issue
Closes #x (replace 'x' with issue number)

- Notes
Anything else to know?
```

6. Once the pull request is reviewed and merged, delete your branch

## Project Scope

### The Goal

The goal of the project is to provide help to someone in a community when they are going through a tough time such as having a new baby, illness, loss, major surgery. A meal train allows friends, families, and neigbors sign up to bring meals for specific days so that the person in need does not have to worry about cooking.

### In Scope Features (MVP)

The features below are must have features for the application to achieve the desired goal:

**Authentication**

- User registration
- User login

**User Dashboard**

- View created meal trains by the user
- View meal trains joined by the user
- Create a meal trian
- Join a meal train

**Meals**

- Create a meal inside a meal train
  - Meal type: breakfast, lunch, dinner
- View meals for a selected day
- Dipslay meal details
- Approve requests for joining meal trains

### Out of Scope Features (Post-MVP)

The features below are a nice to have for the application, but the application could function without them:

- Notifications or reminders
- Editing or deleting meals
- Searching, adding friends, and viewing friend list
- Social media like posting in order to find and join meal trains (only visible to friends)
- Setting and profile page

### Technical Stack

- Frontend: React (Vite), Tailwindcss
- Backend: Django/ Django Rest Framework (DRF)
- Database: PostgreSQL
- Docker for simplified local development

## 📊 Project Analysis

### Numele Proiectului / Project Name

**Meal Train Coordinator** (cod-name: `amber-wisteria`)

---

### Limbajele Folosite / Languages Used

| Strat / Layer | Limbaj / Language | Framework / Tool | Versiune / Version |
|---|---|---|---|
| Backend API | **Python** | Django | 6.0.1 |
| Backend REST | **Python** | Django Rest Framework (DRF) | 3.15.2 |
| Frontend | **JavaScript** | React | 19.2.0 |
| Frontend Build | **JavaScript** | Vite | 7.2.4 |
| Stilizare / Styling | **CSS** | Tailwind CSS | 4.1.18 |
| Client HTTP | **JavaScript** | Axios | 1.13.5 |
| Rutare Frontend | **JavaScript** | React Router | 7.13.0 |
| Baza de Date / Database | **SQL** | PostgreSQL | (via psycopg2) |
| Autentificare / Auth | **Python** | SimpleJWT | 5.4.0 |
| Documentație API | **Python** | DRF YASG (Swagger/OpenAPI) | — |
| Containerizare | — | Docker / Docker Compose | — |

---

### Ce Făcea Aplicația / What the Application Does

**Meal Train Coordinator** este o aplicație web full-stack care ajută comunitățile să organizeze „trenuri de mâncare" (meal trains) pentru persoanele care trec prin momente dificile: nou-nascut, boală, pierdere, operație majoră etc.

Aplicația permite prietenilor, familiei și vecinilor să se înscrie să aducă mâncare în zile specifice, astfel încât persoana aflată în nevoie să nu trebuiască să se îngrijoreze de gătit.

**Funcționalități principale:**

- **Autentificare**: Înregistrare și autentificare utilizator cu token JWT
- **Dashboard utilizator**: Vizualizarea trenurilor de mâncare create sau la care s-a alăturat
- **Creare Meal Train**: Formular în mai mulți pași pentru crearea unui tren de mâncare (tip mâncare: mic dejun, prânz, cină)
- **Sistem de aprobare**: Organizatorul aprobă sau respinge cererile de alăturare
- **Programare mese**: Sloturi de mâncare pe zile și tipuri de mese; calendar interactiv
- **Sistem de prieteni**: Trimitere/acceptare/respingere cereri de prietenie; auto-acceptare mutuală
- **Notificări**: Popup-uri pentru notificări în aplicație

---

### Concepte Importante Folosite / Key Concepts Used

#### 🏛️ OOP (Object-Oriented Programming)
- Modele Django ca clase Python cu relații (`ForeignKey`, `OneToOneField`, `ManyToMany`)
- Vizualizări bazate pe clase (`APIView`, `generics`) în Django Rest Framework
- Componente React (clase și funcționale)

#### 🗄️ Baze de Date / Databases
- **PostgreSQL** ca bază de date relațională
- Design schema relațional: `MealTrain`, `MealSlot`, `MealTrainMembership`, `MealSignup`, `Profile`, `FriendRequest`
- Constrângeri de unicitate (`unique_together`) pentru prevenirea duplicatelor
- Ștergeri în cascadă (`CASCADE`) pentru integritate referențială
- Check constraints pentru validarea stărilor permise

#### 🔐 Autentificare & Autorizare / Authentication & Authorization
- **JWT (JSON Web Tokens)**: autentificare stateless cu access token + refresh token
- **Interceptori Axios**: reîmprospătare automată a token-ului la eroare 401
- **Permisiuni personalizate**: clase de permisiuni DRF (`is_organizer`, `is_allowed_participant`)
- **Rute protejate**: `PrivateRoutes` și `GuestRoutes` în React Router

#### 🌐 REST API Architecture
- Endpoints RESTful: `GET`, `POST`, `PUT`, `PATCH`, `DELETE`
- Resurse imbricate: `/mealtrains/{id}/slots/`, `/mealtrains/{id}/memberships/`
- Serializare și validare date cu DRF Serializers
- Documentație Swagger/OpenAPI automată

#### 🔄 Design Patterns
- **Signal Pattern**: Crearea automată a profilului utilizatorului la înregistrare (Django signals)
- **State Machine**: Flux de stări pentru cereri de membership (`PENDING` → `APPROVED` / `REJECTED`)
- **Component-Based Architecture**: Componentele React reutilizabile (carduri, popup-uri, formulare)
- **Multi-step Form Pattern**: Formular de creare meal train cu pași: `BasicInfoStep` → `ScheduleStep` → `ReviewStep`
- **Repository/Serializer Pattern**: Separarea logicii de serializare de cea a vizualizărilor

#### 🧮 Algoritmi & Logică / Algorithms & Logic
- **Auto-acceptare cereri mutuale de prietenie**: Dacă doi utilizatori și-au trimis reciproc cereri, ambele se acceptă automat
- **Filtrare și validare**: Sloturi duplicate prevenite prin constrângeri de baze de date și validare în serializer
- **Ștergere în cascadă**: Ștergerea unui meal train șterge automat toate sloturile, membership-urile și înscrierile asociate
- **Rutare cu gardă (Route Guards)**: Utilizatorii neautentificați sunt redirecționați automat

#### 🐳 DevOps & Deployment
- **Docker & Docker Compose**: Containerizarea serviciilor (backend + baza de date)
- **Environment Variables**: Configurație prin variabile de mediu pentru portabilitate
- **CORS**: Politici de acces cross-origin configurate

---

## 👥 Team

Leadership

<ul>
  <li><a href="https://github.com/neonbit101">Ruthwik</a></li>
  <li><a href="https://github.com/AnarAskar">Anar</a></li>
</ul>

Participants

<ul>
  <li><a href="https://github.com/JoaquinVeraOrtega">Joaquin</a></li>
  <li><a href="https://github.com/AksharGoyal">Akshar</a></li>
  <li><a href="https://github.com/anthonbrooks">Anthony</a></li>
  <li><a href="https://github.com/akaneme">Akaneme</a></li>
  <li><a href="https://github.com/Bilalnasir057558">Bilal</a></li>
  <li><a href="https://github.com/Lorevdh">Lore</a></li>
  <li><a href="https://github.com/mihaimiron1">Mihai</a></li>
</ul>
