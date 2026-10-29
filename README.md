🚀 ShareNet — Real-Time Communication & File Sharing Platform

ShareNet is a full-stack communication platform that brings user authentication, real-time communication, file sharing, and audio/video calling together in one application.

The project uses React and Vite for the frontend, Node.js and Express for the backend, MongoDB Atlas for data storage, Socket.IO for real-time communication, and Twilio for audio/video calling.

🌐 Live Demo

Live Application: https://sharenet-nu.vercel.app

GitHub Repository: https://github.com/TanveeerSingh/ShareNet

✨ Features

🔐 User Authentication

* User registration and login.
* Password hashing.
* JWT-based authentication.
* Clear feedback for authentication errors.

💬 Real-Time Communication

* Real-time communication using Socket.IO.
* User presence and online status updates.
* Backend support for real-time events.

📁 File Sharing

* File-sharing functionality within the application.
* Support for sharing files through the application’s interface.

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
Real-Time Communication	Socket.IO
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
                  └────────────┬────────────┘
                               │
                         HTTPS / API
                               │
                               ▼
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

📂 Project Structure

ShareNet/
├── backend/
│   ├── config/
│   ├── controllers/
│   ├── models/
│   ├── routes/
│   ├── signaling/
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
│   └── package.json
│
└── README.md

🚀 Getting Started

Follow these instructions to run ShareNet locally.

Prerequisites

Install or prepare the following:

* Node.js and npm
* A MongoDB Atlas account and database.
* A Twilio account with the required credentials.
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

* Use your own MongoDB Atlas connection string.
* Configure your MongoDB Atlas network access to permit connections from your development environment and deployed backend.
* Use the appropriate Twilio credentials for audio/video calling.
* Never commit .env files, database credentials, JWT secrets, or Twilio secrets to GitHub.
* The deployed backend uses environment variables configured in Render.

Start the backend:

npm start

The local backend should be available at:

http://localhost:5001

3. Configure the Frontend

Open a second terminal window and navigate to the frontend directory:

cd ~/Downloads/sharenet-main/softwareproject
npm install

Create a .env.local file inside softwareproject:

VITE_BACKEND_URL=http://localhost:5001

This setting tells the frontend which backend server to communicate with during local development.

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

Redeploy the frontend after changing its environment variables.

Render

Configure the required backend environment variables in the Render service’s environment settings:

* MONGO_URI
* JWT_SECRET
* TWILIO_ACCOUNT_SID
* TWILIO_API_KEY_SID
* TWILIO_API_KEY_SECRET

Render provides the PORT environment variable for the running service. The application should use that value when deployed.

Do not use local development URLs in production configuration.

🔌 API Endpoints

The backend exposes authentication endpoints under /api/users.

Method	Endpoint	Purpose
POST	/api/users/register	Register a new user
POST	/api/users/login	Authenticate an existing user

Example: Registration

Request

POST /api/users/register
Content-Type: application/json
{
  "name": "Example User",
  "email": "user@example.com",
  "password": "your_password"
}

A successful registration returns the created user’s information and an authentication token.

Example: Login

Request

POST /api/users/login
Content-Type: application/json
{
  "email": "user@example.com",
  "password": "your_password"
}

A successful login returns the authenticated user’s information and token.

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

Automatic deployments depend on the hosting services’ GitHub integration and deployment settings.

🔒 Security Notes

* Passwords are hashed before being stored.
* Authentication uses JSON Web Tokens.
* Environment variables are used for sensitive configuration.
* API errors are returned in JSON format without exposing internal stack traces to clients.
* Production secrets must remain in the hosting provider’s environment settings.
* Never publish real database connection strings, authentication tokens, API keys, or passwords.

💡 Technical Highlights

* Full-stack development with React, Node.js, and Express.
* REST API development for user authentication.
* MongoDB integration using Mongoose.
* JWT-based authentication and password hashing.
* Real-time communication using Socket.IO.
* Third-party API integration for audio/video calling.
* Environment-based configuration for local development and production.
* Independent frontend and backend deployment.

🔮 Future Enhancements

Potential improvements include:

* Group messaging and group calls.
* Read receipts and message reactions.
* Message search.
* Screen sharing.
* File transfer progress indicators.
* Improved mobile responsiveness.
* Additional account and session management features.

👨‍💻 Author

Tanveer Singh

* GitHub: TanveeerSingh
* LinkedIn: Tanveer Singh

⸻

If you find this project interesting, consider giving the repository a ⭐ on GitHub.