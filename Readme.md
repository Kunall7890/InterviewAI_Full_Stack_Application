A full-stack interview preparation app using Google Gemini GenAI, MongoDB, and modern React.

## Project scope
- Backend: Node.js + Express + MongoDB + JWT + bcrypt + @google/genai
- Frontend: React + Vite + Context + Protected Routes
- Features: user registration/login, interview report generation, skill gap analysis, question recommendations, preparation plan.

## Folder structure
\`\`\`
interview-ai-yt
├── Backend
│   ├── .env
│   ├── package.json
│   ├── server.js
│   ├── src
│   │   ├── app.js
│   │   ├── config
│   │   │   └── database.js
│   │   ├── controllers
│   │   │   ├── auth.controller.js
│   │   │   └── interview.controller.js
│   │   ├── middlewares
│   │   │   ├── auth.middleware.js
│   │   │   └── file.middleware.js
│   │   ├── models
│   │   │   ├── blacklist.model.js
│   │   │   ├── interviewReport.model.js
│   │   │   └── user.model.js
│   │   ├── routes
│   │   │   ├── auth.routes.js
│   │   │   └── interview.routes.js
│   │   └── services
│   │       └── ai.service.js
│   └── README.md
└── Frontend
    ├── package.json
    ├── vite.config.js
    ├── public/
    ├── src
    │   ├── App.jsx
    │   ├── main.jsx
    │   ├── app.routes.jsx
    │   ├── style.scss
    │   ├── features
    │   │   ├── auth
    │   │   │   ├── auth.context.jsx
    │   │   │   ├── hooks/useAuth.js
    │   │   │   ├── pages/Login.jsx
    │   │   │   ├── pages/Register.jsx
    │   │   │   └── services/auth.api.js
    │   │   └── interview
    │   │       ├── interview.context.jsx
    │   │       ├── hooks/useInterview.js
    │   │       ├── pages/Home.jsx
    │   │       ├── pages/Interview.jsx
    │   │       ├── services/interview.api.js
    │   │       └── style
    │   │           ├── home.scss
    │   │           └── interview.scss
    │   └── style/button.scss
\`\`\`

## Backend setup

1. \\`cd Backend\\`
2. \\`npm install\\`
3. Create \\`.env\\` at \\`Backend/.env\\`:
\\`
GOOGLE_GENAI_API_KEY=<your-google-genai-api-key>
MONGO_URI=mongodb+srv://<user>:<pass>@interviewai.bj9qcac.mongodb.net/interview_ai?retryWrites=true&w=majority
JWT_SECRET=<your-secret>
\\`
4. Start backend:
- \\`npm run dev\\` (recommended)
- or \\`node server.js\\`

5. Ensure network access for Atlas:
- Atlas -> Network Access -> Add IP Address (or 0.0.0.0/0 for dev)

6. Verify endpoints:
- \\`POST /api/auth/register\\`
- \\`POST /api/auth/login\\`
- \\`GET /api/auth/me\\` (requires token cookie)
- \\`POST /api/interview\\` (AI report generation)

## Frontend setup

1. \\`cd Frontend\\`
2. \\`npm install\\`
3. \\`npm run dev\\`
4. Ensure proxy in \\`vite.config.js\\` for \\`/api\\` to \\`http://localhost:3000\\`

## Demo user (quick sign-in)
Register from UI or create manually:
- username: \\`demo\\`
- email: \\`demo@example.com\\`
- password: \\`Demo@1234\\`

Then login with email/password above.

## How GenAI is used

- Backend service: \\`src/services/ai.service.js\\` uses \\`@google/genai\\`.
- \\`GoogleGenAI\\` client is initialized with \\`process.env.GOOGLE_GENAI_API_KEY\\`.
- Interview endpoint takes candidate input (resume, job details) and returns:
  - \\`matchScore\\`, \\`technicalQuestions\\`, \\`behavioralQuestions\\`, \\`skillGaps\\`, \\`preparationPlan\\`.
- Schema validated with \\`zod\\` in \\`interviewReport\\` model.

## Auth flow

- Register: hash password with \\`bcryptjs\\`, create user, issue JWT cookie.
- Login: validate credentials, issue JWT cookie.
- Protected routes: \\`auth.middleware\\` verifies token and checks blacklist.

## Troubleshooting
- \\`API key must be set\\` -> missing \\`GOOGLE_GENAI_API_KEY\\`
- \\`ECONNREFUSED _mongodb._tcp...\\` -> whitelist IP + cluster running
- \\`Invalid email or password\\` -> check DB records
- \\`JWT_SECRET\\` missing -> auth failing

## Useful commands
- \\`npx nodemon server.js\\` (backend auto-reload)
- \\`npm run dev\\` (frontend)
- \\`nslookup -type=SRV _mongodb._tcp.interviewai.bj9qcac.mongodb.net\\`

## Notes
- Keep \\`.env\\` secrets private
- Use local Mongo for offline dev if Atlas is blocked
- \\`0.0.0.0/0\\` in Atlas is for development only
`;
fs.writeFileSync('Readme.md', content, 'utf8');
console.log('Readme.md written');
NODE