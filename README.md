# SENBackend

A Spring Boot backend for the SEN card game, featuring REST APIs, JWT authentication, game session management, AI opponents, and machine learning–powered player profiling.

## Features

- **User Authentication:** JWT-based login, registration, and user management.
- **Game Logic:** Full game session lifecycle, deck management, player actions (draw, swap, skip, wake-up).
- **AI Opponents:** Three types—random, heuristic, and ML-based (Weka decision tree).
- **Machine Learning:** Player move recording, training pipeline, and personalized player profiles using clustering.
- **REST API:** Endpoints for game actions, user management, and profile retrieval.
- **PostgreSQL Integration:** Persistent storage for users, games, moves, and profiles.
- **Docker Compose:** Easy local setup for backend and database.

## Getting Started

### Prerequisites

- Java 17+
- Maven
- Docker (for PostgreSQL)
- Git

### Setup

1. **Clone the repository:**
   ```sh
   git clone <your-repo-url>
   cd SenBackend
   ```

2. **Start PostgreSQL with Docker Compose:**
   ```sh
   docker compose -f compose.yaml up -d
   ```

3. **Build the project:**
   ```sh
   ./mvnw clean package
   ```

4. **Run the backend:**
   ```sh
   ./mvnw spring-boot:run
   ```
   Or:
   ```sh
   java -jar target/SenBackend-0.0.1-SNAPSHOT.jar
   ```

### Configuration

Edit `src/main/resources/application.properties` to set database credentials, JWT secrets, and other settings.

## Machine Learning: Player Profiles

The backend computes per-player aggregates (win rate, average score, swap/skip rates, risk score) and clusters players using Weka KMeans. Profiles are stored in the `player_profiles` table and used to personalize AI behavior.

**Key files:**
- `profiles/PlayerProfile.java` — JPA entity for player profiles.
- `profiles/PlayerFeatureExtractor.java` — Computes per-player features from DB.
- `profiles/PlayerProfileTrainingService.java` — Trains clusters and persists profiles.
- `profiles/PlayerProfileController.java` — API endpoints for profile retrieval and retraining.

## API Endpoints

- `POST /api/auth/login` — Login and receive JWT.
- `POST /api/auth/register` — Register new user.
- `GET /api/game/{id}` — Get game state.
- `POST /api/game/{id}/action` — Perform game action.
- `GET /api/player/{playerId}/profile` — Get player profile (ML cluster).
- `POST /api/player/admin/retrain` — Retrain player profiles (admin only).

See [API documentation](docs/) for full details.

## Development

- Code is organized by domain: `login/`, `gamelogic/`, `ai/`, `profiles/`.
- Uses Spring Data JPA for persistence.
- ML logic uses Weka (see `pom.xml` for dependency).

## Testing

- Unit and integration tests use JUnit and Testcontainers.
- Run tests:
  ```sh
  ./mvnw test
  ```

## Contributing

1. Fork the repo and create your branch.
2. Make changes and commit.
3. Submit a pull request.

## License

MIT (or specify your license).

---

**Contact:** [Your Name] — [your.email@example.com]




