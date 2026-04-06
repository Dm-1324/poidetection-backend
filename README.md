POI Detector: Smart Location Assistant
A full-stack application that monitors user movement in real-time, identifies nearby Points of Interest (POIs) such as restaurants, fuel stations, and malls using the Overpass API, and sends personalized notifications based on a 3-hour cooldown logic.

🚀 Features
Real-time Tracking: Background geolocation monitoring at 30-second intervals.

POI Detection: Automated discovery of nearby amenities via OpenStreetMap (Overpass API).

Smart Notifications: "Welcome" alerts with persistent state management to prevent notification fatigue (3-hour cooldown per POI).

Consent-First Design: Users must explicitly grant location tracking consent before the service activates.

Manual Override: A dedicated testing interface to simulate coordinates and verify detection logic.

Mobile Responsive: Fully adaptive UI designed for both desktop and mobile devices using CSS Grid.

🛠️ Tech Stack
Backend
Framework: Spring Boot 3.5.11

Database: PostgreSQL (Hosted on Supabase)

Security: Spring Security with custom CORS configuration

ORM: Spring Data JPA

Frontend
Framework: Vue 3 (Composition API)

HTTP Client: Axios

Styling: Modern CSS with Flexbox/Grid

⚙️ Setup & Installation
1. Backend Configuration
Ensure you have Java 17 installed.

Environment Variables: Configure your Supabase connection using the Transaction Pooler (Port 6543) for stability.

Variable	Value
SPRING_DATASOURCE_URL	jdbc:postgresql://[host]:6543/postgres?sslmode=require
SPRING_DATASOURCE_USERNAME	postgres.[YOUR_PROJECT_REF]
SPRING_DATASOURCE_PASSWORD	[YOUR_PASSWORD]
Run Application:

Bash
./mvnw spring-boot:run
2. Frontend Configuration
Ensure you have Node.js installed.

Update API URL: Set the baseURL in src/services/api.js to your Railway or local backend URL.

Install Dependencies:

Bash
npm install
Run Development Server:

Bash
npm run dev
🏗️ Architecture
Frontend: Captures Geolocation and sends it to the backend.

Backend: Validates user consent and queries the Overpass API.

Third-Party API: Overpass interprets the coordinates and returns nearby amenities.

Database: Persists user registration and tracking history (UserPoiState) to Supabase.

🛠️ Key Bug Fixes & Refinements
CORS Conflicts: Centralized CORS configuration in SecurityConfig to prevent "Multiple Values" header errors.

Transaction Management: Applied @Transactional to UserPoiStateRepository to resolve TransactionRequiredException during user session resets.

API Resilience: Implemented ResourceAccessException handling for Overpass API to provide user-friendly "Server not responding" feedback during high-traffic periods.

📬 API Endpoints
Method	Endpoint	Description
POST	/auth/register	Create a new user account
POST	/auth/login	Authenticate and reset current POI state
POST	/auth/consent	Update user location tracking consent
POST	/location/update	Process coordinates and check for POIs
