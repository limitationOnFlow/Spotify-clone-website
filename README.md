### Architectural Highlights
* **Decoupled Client-Server Model:** Client-side application handles UI rendering and persistent audio state, while the backend handles authentication, business logic, and database operations.
* **Content Delivery Network (CDN) Integration:** Audio tracks and high-resolution cover arts are offloaded to cloud object storage (AWS S3) and distributed worldwide via CloudFront for low-latency playback.
* **Persistent Audio Pipeline:** Global state machine ensuring audio playback remains uninterrupted during client-side page transitions and sub-route navigation.

---

## Core Feature Specifications

### 1. User Authentication & Security System
* **Multi-Factor Authentication Flow:** Support for email/password credentials and third-party OAuth 2.0 single sign-on (Google, GitHub, Spotify API).
* **Token-Based Authorization:** Secure authentication using stateless **JSON Web Tokens (JWT)** stored in HttpOnly, SameSite cookies to protect against XSS and CSRF attacks.
* **Role-Based Access Control (RBAC):**
  * **Listener Role:** Stream audio, create playlists, like songs, follow artists.
  * **Artist Role:** Access upload portal, manage track metadata, view basic listener analytics.
  * **Admin Role:** Moderation dashboard, user management, system diagnostics.

### 2. High-Performance Audio Playback Engine
* **Persistent Audio Control Bar:**
  * Play, pause, skip forward/backward, and shuffle algorithms (Fisher-Yates shuffle).
  * Repeat track modes (Off, Repeat All, Repeat One).
  * Scrubbing/seeking bar with dynamic buffering indicators.
  * Real-time volume slider with quick-mute toggle and persistent preference caching.
* **Queue & Context Management:**
  * Dynamic playback queue allowing manual track insertion ("Play Next", "Add to Queue").
  * Context-aware playback (playing from album context, playlist context, or liked songs context).
* **Adaptive Streaming & Preloading:**
  * HTML5 Audio API / Howler.js integration handling audio buffering, error recovery, and seamless gapless playback transitions.

### 3. Media & Content Discovery
* **Dynamic Search Engine:** Debounced search interface querying tracks, artists, albums, and user-generated playlists with instant auto-suggestions.
* **Categorized Browse Hub:** Genre and mood grid (e.g., Pop, Hip-Hop, Chill, Focus, Workout) auto-populating curated playlists.
* **Full-Featured Library:** Custom sections for "Liked Songs", "Saved Albums", "Followed Artists", and "User Playlists".

### 4. Playlist & Library Curation
* **CRUD Playlist Management:** Create, update metadata (title, cover image, description), reorder tracks, and delete custom playlists.
* **Collaborative Playlists:** Real-time playlist editing using WebSockets where multiple users can contribute tracks concurrently.
* **Dynamic Track Liking:** One-click favorite toggling that automatically syncing with the user's dedicated "Liked Songs" repository.

### 5. Creator / Artist Dashboard
* **Audio & Image Upload Pipeline:** Drag-and-drop file upload with client-side validation (file size, format checks for `.mp3`, `.wav`, `.jpg`, `.png`).
* **Metadata Editor:** Tagging systems for track title, genre, explicit content flags, release date, and album assignment.

---

## Technology Stack & Tooling

| Component | Technology | Purpose |
| :--- | :--- | :--- |
| **Frontend Framework** | Next.js 14 / React 18 | SSR/SSG rendering, routing, and UI components |
| **Language** | TypeScript | End-to-end type safety and maintainable codebase |
| **Styling & UI** | Tailwind CSS + Shadcn UI | Utility-first dark theme styling and sleek accessibility |
| **State Management** | Zustand / Redux Toolkit | Global persistent player state, queue management, and auth context |
| **Backend Runtime** | Node.js (Express.js) | RESTful API backend and middleware pipeline |
| **Database** | PostgreSQL / MongoDB | Persistent relational data model for users, tracks, playlists |
| **ORM / ODM** | Prisma / Mongoose | Schema validation, migrations, and typed database queries |
| **Cloud Storage** | AWS S3 / Cloudinary | Secure hosting for audio binaries and image media assets |
| **Real-Time Layer** | Socket.IO | Collaborative playlist updates and synchronized listening |
| **Testing** | Jest + React Testing Library | Unit and integration testing suites |

---

## Database Schema Design

### Entity-Relationship Diagram Overview

# Server Configuration
PORT=5000
NODE_ENV=development

# Database
DATABASE_URL="postgresql://user:password@localhost:5432/spotify_db?schema=public"

# Authentication Secrets
JWT_SECRET="your_super_secret_jwt_key_here"
NEXTAUTH_SECRET="your_next_auth_secret_key"
NEXTAUTH_URL="http://localhost:3000"

# Cloud Media Storage (AWS S3)
AWS_ACCESS_KEY_ID="YOUR_AWS_ACCESS_KEY"
AWS_SECRET_ACCESS_KEY="YOUR_AWS_SECRET_KEY"
AWS_REGION="us-east-1"
AWS_S3_BUCKET_NAME="spotify-clone-media-bucket"



