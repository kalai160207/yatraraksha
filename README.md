YatraRaksha – Smart Tourist Safety PlatformTagline: Travel Safe. Stay Connected. Respond Faster.YatraRaksha is an intelligent, real-time tourist safety and emergency response ecosystem designed to protect travelers, enable proactive hazard monitoring, and empower command center operators with instant incident management capabilities.📌 Table of ContentsOverviewKey FeaturesSystem Architecture & RolesTech StackProject File StructureGetting Started & InstallationPrerequisitesEnvironment VariablesBackend & Admin SetupFrontend SetupCore Workflows & Features1. Tourist Registration & Digital ID2. Trip Lifecycle Management3. SOS Emergency System4. Super Admin Command Center5. Gemini AI Safety Assistant6. Blockchain-Inspired Audit LedgerSecurity ArchitectureDemo ProcessMultilingual SupportLicense🛡️ OverviewYatraRaksha bridges the critical gap between tourists and emergency response networks. By pairing continuous GPS safety telemetry, dynamic geofencing hazard alerts, digital pass generation, and real-time Socket.IO communication, YatraRaksha delivers immediate visibility and faster emergency resolution times.✨ Key Features🆔 Digital Tourist Identity (YR-2026-XXXXXX): Automated unique ID generation with dynamic QR verification codes.📍 Live Geolocation Tracking & Consent: Granular location sharing controls powered by browser Geolocation APIs (watchPosition).🗺️ Interactive Command Center Map: OpenStreetMap & Leaflet integration rendering color-coded tourist status markers (SAFE, ATTENTION, EMERGENCY, OFFLINE).🚨 One-Touch SOS Emergency Response: Instant location dispatch generating incident codes (SOS-2026-XXXXXX) and alerting command center operators without page refresh.🧳 Trip & Itinerary Lifecycle: Register trip destinations, list points of interest/attractions, track visited spots, mark trips as finished, and safely delete completed trips.🤖 YatraRaksha AI Assistant: Contextual safety advice, first-aid procedures, and local emergency guidance powered by Google Gemini API.⛓️ Prototype Blockchain Audit Ledger: Cryptographic SHA-256 hash-chained event logger ensuring non-repudiation for security and incident logs.🌐 Multilingual Interface: Seamless instant translation between English and தமிழ் (Tamil).👤 System Architecture & RolesThe system enforces strict role-based authorization:                  ┌────────────────────────┐
                  │      SUPER_ADMIN       │
                  │ (Command Center Op:    │
                  │   Kalaiyarasan)        │
                  └───────────┬────────────┘
                              │
         ┌────────────────────┴────────────────────┐
         ▼                                         ▼
┌──────────────────┐                     ┌───────────────────┐
│     TOURISTS     │                     │ EMERGENCY_         │
│ (Self-registered │                     │ RESPONDERS        │
│  mobile/web)     │                     │ (Assigned units)  │
└──────────────────┘                     └───────────────────┘
SUPER_ADMIN (Single Authority):Command operator: KalaiyarasanFull command center access, live global tourist tracking, SOS incident response, responder assignment, security audit logs, session revocation.Strict Rule: Only ONE Super Admin account can exist in the system (enforced by partial database index and backend creation script).TOURIST (Public Travelers):Can register accounts, view digital ID & QR codes, manage itineraries/trips, toggle live location sharing, ask the AI assistant, trigger SOS alerts, and view personal history.EMERGENCY_RESPONDER:Field personnel assigned to specific active SOS incidents.💻 Tech StackFrontendFramework: React.js + Vite (JavaScript / TypeScript)Styling: Tailwind CSS (Dark Command-Center Theme & Glassmorphism)Icons: Lucide ReactMapping: Leaflet & React-Leaflet + OpenStreetMapReal-Time Data: Socket.IO ClientHTTP Client: AxiosQR Code: Canvas / Inline SVG GeneratorBackend (Architecture Standard)Runtime: Node.js & Express.jsReal-time Engine: Socket.IODatabase: MongoDB & MongooseAuthentication: JWT + HTTP-only Secure CookiesSecurity: Helmet, CORS, Express-Rate-Limit, bcrypt / Argon2idAI Integration: Google Gemini API (Backend Proxied)📁 Project File Structureyatraraksha/
├── backend/
│   ├── src/
│   │   ├── config/          # DB, Socket.IO & Gemini configurations
│   │   ├── controllers/     # Auth, Tourist, SOS, Admin controllers
│   │   ├── middleware/      # Auth, Admin validation, Rate limiters
│   │   ├── models/          # Mongoose Schemas (User, SOS, Audit, Trip)
│   │   ├── routes/          # API endpoints (/api/auth, /api/admin, etc.)
│   │   ├── scripts/         # create-admin.js setup script
│   │   └── server.js        # Express application entry point
│   ├── .env.example
│   └── package.json
│
├── frontend/
│   ├── src/
│   │   ├── components/      # UI Cards, Digital ID, SOS Modals, Map View
│   │   ├── context/         # Auth & Language Contexts
│   │   ├── hooks/           # Geolocation & Socket hooks
│   │   ├── App.jsx          # Main Web Application Component
│   │   └── main.jsx
│   ├── index.html
│   ├── tailwind.config.js
│   └── package.json
└── README.md
🚀 Getting Started & InstallationPrerequisitesNode.js (v18.x or higher)MongoDB running locally or a MongoDB Atlas connection stringnpm or yarnEnvironment VariablesCreate a .env file in your backend/ directory based on .env.example:PORT=5000
CLIENT_ORIGIN=http://localhost:5173
MONGODB_URI=mongodb://localhost:27017/yatraraksha
JWT_SECRET=your_super_secret_jwt_key_here
GEMINI_API_KEY=your_gemini_api_key_here
ADMIN_ALERT_PHONE=+919876543210
ADMIN_ALERT_EMAIL=admin@yatraraksha.gov.in
TWILIO_ACCOUNT_SID=
TWILIO_AUTH_TOKEN=
TWILIO_FROM_PHONE=
CRITICAL SECURITY NOTE: Never prefix admin credentials or private API keys with VITE_. All sensitive keys must remain strictly on the backend.Backend & Admin SetupInstall dependencies:cd backend
npm install
Initialize Super Admin (Kalaiyarasan):
Run the interactive initialization script to set up the unique Super Admin account securely:npm run create-admin
Prompt responses:Admin Name: KalaiyarasanAdmin Role: SUPER_ADMINPassword: [Strong Password]Start Backend Server:npm run dev
Frontend SetupInstall dependencies:cd frontend
npm install
Start Development Client:npm run dev
Open http://localhost:5173 in your browser.🔄 Core Workflows & Features1. Tourist Registration & Digital IDTourists register with Name, Phone, Date of Birth, Emergency Contact, and Nationality.Location Permission Prompt: Explicitly requests browser location access before completing registration.Automated ID Assignment: System creates identity tokens like YR-2026-000421.Digital Pass & QR: Generates a verifiable identity card and QR code containing ID, status, and verification timestamp.2. Trip Lifecycle ManagementRegister New Trip: Add destination name, region, dates, emergency contact, and points of interest (attractions).Visited Place Checklist: Toggle individual attractions as visited during travel.Finish Trip: Mark trips as completed once travel ends.Delete Trip: Clean up finished or redundant trips with a confirmation dialog.3. SOS Emergency SystemTourist presses 🚨 SEND SOS.Confirmation popup displays warning and captures live GPS coordinates.System assigns incident code (SOS-2026-XXXXXX).Socket.IO broadcasts sos:new to Command Center instantly.Command Center operator views tourist location, safety score drop, and assigned emergency contact.Operator updates incident lifecycle: ACTIVE → RESPONDING → RESOLVED.4. Super Admin Command CenterOperated by Kalaiyarasan.Metrics Bar: Active SOS, Safe Tourists, Total Registered, Responders, High-Risk Geofences.Live Command Map: Real-time Leaflet map displaying active tourist coordinates and geofence caution zones.Incident Dispatch & Responder Assignment: Direct action buttons to assign responders and handle emergencies.5. Gemini AI Safety AssistantIntegrated with backend Gemini API endpoint /api/ai/ask.Answers queries regarding:Local emergency contact numbersFirst-aid guidance for minor injuries/heatstrokesSafe traveling advice for specific regionsWhat to do if lost or separated from a tour group6. Blockchain-Inspired Audit LedgerCaptures critical state events: TOURIST_REGISTRATION, LOCATION_TOGGLE, SOS_TRIGGERED, RESPONDER_ASSIGNED, EMERGENCY_RESOLVED, ADMIN_LOGIN.Every block stores Block ID, Timestamp, Event, User ID, Hash, and Previous Hash calculated using SHA-256 chaining.🔒 Security ArchitectureSecurity DomainImplementation StandardAuthenticationJWT stored in HTTP-only, SameSite, Secure cookiesPassword HashingBcrypt with cost factor 12 / Argon2idRole AuthorizationBackend middleware verifies role === 'SUPER_ADMIN' for /api/admin/*Single Admin RuleMongoDB partial unique index prevents duplicate SUPER_ADMIN creationData PrivacyTourist A cannot access Tourist B's location, phone, or identity recordsLocation Opt-OutTurning location sharing OFF immediately halts client geolocation transmissionsRate LimitingExpress Rate Limit protects login and SOS dispatch endpoints🧪 Demo ProcessOpen Application: Navigate to http://localhost:5173.Tourist Flow:Click "சுற்றுலா பயனர் பதிவு" / "Tourist Profile".Fill in details for a new tourist (e.g. Arun Kumar).Grant Geolocation permission & click "Register & Activate Location".Observe generated ID (e.g., YR-2026-000421).Trip Registration:Click "+ புதிய பயணம் பதிவு செய்" / "+ Register New Trip".Destination: Madurai Heritage & Temple Circuit, add attractions (Meenakshi Temple, Nayakkar Palace).Toggle visited places. Once done, test Finish Trip and Delete Trip buttons.Emergency SOS Flow:Click "அவசர உதவி SOS" / "Trigger SOS Alert".Confirm SOS generation. Observe status change to EMERGENCY.Command Center Flow:Switch role to Super Admin Command Center (Kalaiyarasan).Locate the red marker on the Live Map.Assign responder, change status to RESPONDING, then mark RESOLVED.Audit Ledger:Review SHA-256 block hash records in the audit ledger tab.🌐 Multilingual SupportThe entire application provides instant UI switching between:🇬🇧 English🇮🇳 தமிழ் (Tamil)Toggle language anytime using the language selector button in the top navigation bar.📄 LicenseThis project is released under the MIT License.YatraRaksha – Travel Safe. Stay Connected. Respond Faster.
