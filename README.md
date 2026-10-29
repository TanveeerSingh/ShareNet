# 🚀 ShareNet — Real-Time Communication & File Sharing Platform

![React](https://img.shields.io/badge/React-Frontend-61DAFB?logo=react&logoColor=black)
![Vite](https://img.shields.io/badge/Vite-Build%20Tool-646CFF?logo=vite&logoColor=white)
![Node.js](https://img.shields.io/badge/Node.js-Backend-339933?logo=node.js&logoColor=white)
![Express](https://img.shields.io/badge/Express.js-API-000000?logo=express&logoColor=white)
![MongoDB](https://img.shields.io/badge/MongoDB-Database-47A248?logo=mongodb&logoColor=white)
![Socket.IO](https://img.shields.io/badge/Socket.IO-Real--Time-010101?logo=socket.io&logoColor=white)
![Twilio](https://img.shields.io/badge/Twilio-Audio%20%26%20Video-F22F46?logo=twilio&logoColor=white)
![Render](https://img.shields.io/badge/Render-Backend%20Hosting-46E3B7?logo=render&logoColor=black)
![Vercel](https://img.shields.io/badge/Vercel-Frontend%20Hosting-black?logo=vercel&logoColor=white)
# 🚀 ShareNet — Real-Time Communication & File Sharing Platform

![React](https://img.shields.io/badge/React-Frontend-61DAFB?logo=react&logoColor=black)
![Vite](https://img.shields.io/badge/Vite-Build%20Tool-646CFF?logo=vite&logoColor=white)
![Node.js](https://img.shields.io/badge/Node.js-Backend-339933?logo=node.js&logoColor=white)
![Express](https://img.shields.io/badge/Express.js-API-000000?logo=express&logoColor=white)
![MongoDB](https://img.shields.io/badge/MongoDB-Database-47A248?logo=mongodb&logoColor=white)
![Socket.IO](https://img.shields.io/badge/Socket.IO-Real--Time-010101?logo=socket.io&logoColor=white)
![Twilio](https://img.shields.io/badge/Twilio-Audio%20%26%20Video-F22F46?logo=twilio&logoColor=white)
![Render](https://img.shields.io/badge/Render-Backend%20Hosting-46E3B7?logo=render&logoColor=black)
![Vercel](https://img.shields.io/badge/Vercel-Frontend%20Hosting-black?logo=vercel&logoColor=white)

ShareNet is a full-stack communication platform that brings user authentication, real-time communication, file sharing, and audio/video calling together in one application.

The project uses React and Vite for the frontend, Node.js and Express for the backend, MongoDB Atlas for data storage, Socket.IO for signalling and presence, WebRTC data channels for peer-to-peer messaging and file transfer, and Twilio for audio/video calling.

🌐 Live Demo

Live Application: https://sharenet-nu.vercel.app

GitHub Repository: https://github.com/TanveeerSingh/ShareNet

✨ Features

🔐 User Authentication

* User registration and login.
* Password hashing with bcryptjs.
* JWT-based authentication (tokens are issued at login/registration; see Security Notes for the current scope).
* Clear feedback for authentication errors, returned by the API as JSON messages.

💬 Real-Time Communication

* Signalling and online presence using Socket.IO.
* One-to-one private messaging over peer-to-peer WebRTC data channels.
* User presence and online status updates.
* Messages are exchanged directly between browsers and are not stored on the server, so both users need to be online at the same time and chat history is not kept.

📁 File Sharing

* File sharing from within the chat interface.
* Files are split into 16 KB chunks, sent over the same peer-to-peer WebRTC connection, and reassembled by the receiver.
* The whole file is handled in browser memory on both sides, so sharing works best for small to moderate file sizes.

📞 Audio and Video Calling

* Audio calling.
* Video calling.
* Twilio-powered communication.
* Backend token generation for Twilio Video.

🖥️ Web Application

* React-based user interface.
* Vite development server and production build.
* Independent frontend and backend deployments.

🛠️ Tech Stack

Category	Technology
Frontend	React.js
Build Tool	Vite
Styling	Tailwind CSS and CSS
Backend	Node.js
Backend Framework	Express.js
Database	MongoDB Atlas
Database ODM	Mongoose
Real-Time Communication	Socket.IO (signalling and presence) and WebRTC (messaging and file transfer)
Authentication	JSON Web Tokens (JWT)
Password Hashing	bcryptjs
Audio/Video Calling	Twilio
Frontend Hosting	Vercel
Backend Hosting	Render

🏗️ Architecture

                  ┌─────────────────────────┐
                  │         Users           │
                  └────────────┬────────────┘
                               │
                               ▼
                  ┌─────────────────────────┐
                  │         Vercel          │
                  │     React + Vite        │
                  └────────┬────────────────┘
                           │
              ┌────────────┼─────────────────────┐
              │            │                     │
        HTTPS / API        │ Socket.IO           │ WebRTC (peer-to-peer)
              │      (signalling/presence)       │ chat, files, and
              ▼            ▼                     ▼ Twilio media for calls
                  ┌─────────────────────────┐
                  │         Render          │
                  │    Node.js + Express    │
                  │       Socket.IO         │
                  └────────┬────────┬───────┘
                           │        │
                    ┌──────▼───┐ ┌──▼────────────┐
                    │ MongoDB  │ │    Twilio     │
                    │  Atlas   │ │ Audio/Video   │
                    └──────────┘ └───────────────┘

Chat messages and files travel directly between the two browsers over a WebRTC data channel; the server only introduces the peers (signalling) and tracks who is online. Call media runs through Twilio after the backend issues a short-lived access token.

📂 Project Structure

ShareNet/
├── backend/
│   ├── config/
│   ├── controllers/
│   ├── models/
│   ├── routes/
│   ├── signaling/          (legacy — currently unused; signalling lives in server.js)
│   ├── utils/
│   ├── loadenv.js
│   ├── server.js
│   └── package.json
│
├── softwareproject/
│   ├── public/
│   ├── src/
│   │   └── components/
│   ├── index.html
│   ├── vite.config.js
│   ├── tailwind.config.js
│   ├── postcss.config.js
│   ├── vercel.json
│   └── package.json
│
├── package.json
└── README.md

🚀 Getting Started

Follow these instructions to run ShareNet locally.

Prerequisites

Install or prepare the following:

* Node.js 20.19 or newer (or 22+) and npm. The frontend uses Vite 7, which does not run on older Node versions.
* A MongoDB Atlas account and database (or any MongoDB connection string for local development).
* A Twilio account with the required credentials — only needed for audio/video calling. Authentication, presence, chat, and file sharing run without valid Twilio credentials.
* Git.

1. Clone the Repository

git clone https://github.com/TanveeerSingh/ShareNet.git
cd ShareNet

2. Configure the Backend

Navigate to the backend directory and install dependencies:

cd backend
npm install

Create a .env file inside the backend directory.

Add the following configuration, replacing the placeholders with your own values:

PORT=5001
MONGO_URI=your_mongodb_connection_string
JWT_SECRET=your_jwt_secret
TWILIO_ACCOUNT_SID=your_twilio_account_sid
TWILIO_API_KEY_SID=your_twilio_api_key_sid
TWILIO_API_KEY_SECRET=your_twilio_api_key_secret

Important:

* PORT is optional. If it is not set, the backend listens on port 8080. The example uses 5001 because the frontend's built-in local fallback is http://localhost:5001, so the two match during local development.
* Always start the backend from inside the backend directory (npm start). The .env file is loaded relative to the directory the server is started from.
* Use your own MongoDB Atlas connection string.
* Configure your MongoDB Atlas network access to permit connections from your development environment and deployed backend.
* Use the appropriate Twilio credentials for audio/video calling.
* Never commit .env files, database credentials, JWT secrets, or Twilio secrets to GitHub.
* The deployed backend uses environment variables configured in Render.

Start the backend:

npm start

With the example configuration above, the local backend is available at:

http://localhost:5001

3. Configure the Frontend

Open a second terminal window. From the repository root, navigate to the frontend directory (if your terminal is still in backend/, use cd ../softwareproject instead):

cd softwareproject
npm install

Create a .env.local file inside softwareproject:

VITE_BACKEND_URL=http://localhost:5001

This setting tells the frontend which backend server to communicate with during local development. If it is not set, the frontend falls back to http://localhost:5001.

Start the frontend:

npm run dev

Vite will display the local development URL, usually:

http://localhost:5173

Open that address in your browser.

4. Production Environment Configuration

The production frontend and backend are configured separately.

Vercel

Configure the following frontend environment variable in your Vercel project:

VITE_BACKEND_URL=https://sharenet-backend-iyyv.onrender.com

Redeploy the frontend after changing its environment variables. Vite variables are applied at build time, so a change has no effect until the next deployment.

Render

Configure the required backend environment variables in the Render service's environment settings:

* MONGO_URI
* JWT_SECRET
* TWILIO_ACCOUNT_SID
* TWILIO_API_KEY_SID
* TWILIO_API_KEY_SECRET

Render provides the PORT environment variable for the running service. The application uses that value when deployed.

Do not use local development URLs in production configuration.

🔌 API Endpoints

The backend exposes authentication endpoints under /api/users, plus a Twilio token endpoint.

Method	Endpoint	Purpose
POST	/api/users/register	Register a new user
POST	/api/users/login	Authenticate an existing user
GET	/twilio/token	Generate a Twilio Video access token (query parameters: identity, room)
GET	/	Service status message

Example: Registration

Request

POST /api/users/register
Content-Type: application/json
{
  "name": "Example User",
  "email": "user@example.com",
  "password": "your_password"
}

A successful registration returns HTTP 201 with the created user's information and an authentication token:

{
  "_id": "user_id",
  "name": "Example User",
  "email": "user@example.com",
  "token": "jwt_token"
}

Example: Login

Request

POST /api/users/login
Content-Type: application/json
{
  "email": "user@example.com",
  "password": "your_password"
}

A successful login returns HTTP 200 with the authenticated user's information and token, in the same format as registration.

Error Handling

The API returns JSON error responses for failed requests.

For example, attempting to register an existing email returns HTTP 400:

{
  "message": "User already exists"
}

An unsuccessful login returns HTTP 401:

{
  "message": "Invalid email or password"
}

Requests to unknown routes return HTTP 404 with a JSON message, and unexpected server errors return HTTP 500 with a generic JSON message. Internal error details and stack traces are logged on the server only and are not sent to clients.

☁️ Deployment

ShareNet uses separate hosting services for the frontend and backend.

Component	Platform
Frontend	Vercel
Backend	Render
Database	MongoDB Atlas
Audio/Video Services	Twilio

Deployment Workflow

1. Push changes to the GitHub repository.
2. Vercel builds and deploys the frontend.
3. Render builds and deploys the backend.
4. Verify that the frontend points to the correct backend URL.
5. Test authentication and other application features after deployment.

Automatic deployments depend on the hosting services' GitHub integration and deployment settings.

🔒 Security Notes

* Passwords are hashed with bcryptjs (salt rounds: 10) before being stored. Plaintext passwords are never stored or returned by the API.
* Authentication uses JSON Web Tokens. Tokens are issued at registration and login, expire after 30 days, and are stored in the browser's localStorage.
* Current scope of token enforcement: the backend does not yet verify JWTs on its routes, protected pages are guarded on the client side, and the Twilio token endpoint does not yet require authentication. Treat the JWT today as proof of login for the UI, not as a server-enforced credential, until backend verification is added.
* All production traffic uses HTTPS/WSS. Chat messages and files are encrypted in transit directly between browsers by the WebRTC data channel (DTLS) and are never stored on the server. Call media is encrypted between each browser and Twilio; calls are not end-to-end encrypted.
* Environment variables are used for sensitive configuration.
* API errors are returned in JSON format without exposing internal stack traces to clients.
* Production secrets must remain in the hosting provider's environment settings.
* Never publish real database connection strings, authentication tokens, API keys, or passwords.

💡 Technical Highlights

* Full-stack development with React, Node.js, and Express.
* REST API development for user authentication.
* MongoDB integration using Mongoose.
* JWT-based authentication and bcryptjs password hashing.
* Real-time signalling and presence using Socket.IO, with peer-to-peer messaging and file transfer over WebRTC data channels.
* Third-party API integration for audio/video calling.
* Environment-based configuration for local development and production.
* Independent frontend and backend deployment.

🔮 Future Enhancements

Potential improvements include:

* Backend verification of JWTs and an authenticated Twilio token endpoint.
* Group messaging and group calls.
* Read receipts and message reactions.
* Message search and stored chat history.
* Screen sharing.
* File transfer progress indicators and support for larger files (streaming instead of in-memory transfer).
* A TURN server for reliable peer connections on restrictive networks.
* Improved mobile responsiveness.
* Additional account and session management features.

👨‍💻 Author

Tanveer Singh

* GitHub: TanveeerSingh
* LinkedIn: Tanveer Singh
