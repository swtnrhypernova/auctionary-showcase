# Auctionary — Full-Stack Auction Platform

> **Note on repository access:** This is the public showcase repository for a university full-stack development project. The original repository contains provided starter code and remains private for academic integrity reasons. This README documents my design decisions and the features I built on top of that starting point. Representative code excerpts are in [`showcase/`](./showcase).

<p align="center">
  <img src="<img width="1470" height="956" alt="auctionary home page" src="https://github.com/user-attachments/assets/89fbe869-9e15-4962-a6f3-35d1d4fedb54" />
" alt="Auctionary homepage" width="700">
</p>

## 🎥 Demo Recording


## What it is

Auctionary is a database-driven auction web application. Users can register, log in, create item listings, browse listings by category, and place bids on other users' items.

**Live demo coming soon** · Built January 2026 as a second-year full-stack development project at Manchester Metropolitan University.

## What I did (and why)

### User authentication & validation
I implemented registration and login from the ground up, including server-side validation (email format, password rules, duplicate-account checks) and session handling. The motivation was to learn how authentication actually works end-to-end rather than delegating it to a library — password storage is handled with salted hashing, never plaintext.

### Content moderation
User-generated titles and descriptions pass through a profanity filter before they reach the database. I added this after considering what happens when an auction platform lets *anyone* write *anything* — a small but real trust and safety problem, and an introduction to input sanitisation as a security mindset.

### Category system
I designed a categorisation scheme so listings are browsable and searchable rather than one undifferentiated list. This required changes across all three layers — a category table in SQLite, filtering endpoints in Express, and category-driven views in Vue — which taught me how one feature ripples through an MVC architecture.

### Bidding
The bidding flow validates that a new bid is higher than the current one and updates the listing in real time for the viewing user.

## How I built it

| Layer | Technology | Notes |
| --- | --- | --- |
| Frontend | Vue.js, Tailwind CSS, HTML5, CSS3 | Component-based UI, form state, category filtering |
| Backend | Node.js, Express.js, RESTful APIs | Route → controller → model separation (MVC) |
| Database | SQLite (better-sqlite3), SQL | Users, listings, bids, categories; parameterised queries throughout |
| Tools | VS Code, Postman, Git, GitHub | API endpoints tested in Postman before wiring the frontend |

### Architecture
The backend follows **MVC principles**: Express routes stay thin, controllers hold the request/response logic, and models own all SQL access. All database calls use **parameterised queries** to prevent SQL injection.

## Challenges & what I learned

- **Validation belongs on the server.** My first validation attempts lived only in the frontend; testing with Postman showed the API happily accepted malformed data. I rewrote validation as backend checks the frontend merely mirrors — my clearest lesson in never trusting client input.
- **One feature, three layers.** Adding categories forced me to touch the schema, four API endpoints, and two Vue components in one coordinated change — a practical lesson in why MVC separation keeps changes tractable.
- **State management across a bid.** Keeping the current-bid display consistent after a successful bid taught me about Vue reactivity and where component state should live.

## What I'd do differently

- Migrate session auth to **JWT-based authentication** to support a future API/mobile client.
- Add **server-side pagination** for listing browsing — the current implementation loads all matching listings.
- Introduce proper **unit tests** (Jest) for the controllers — this project predates my test-first habits.
- Real-time bid updates via **WebSockets** instead of refetching.

## Acknowledgements

Built as coursework for a full-stack web development module at Manchester Metropolitan University. The private original repository began from starter code provided by the module team; all features described above are my own implementation.
