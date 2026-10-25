# ShareNet Project Handoff

## User Goal
Run the ShareNet full-stack project locally on macOS and get the backend working.

## Project Location
`/Users/tanveersingh/Downloads/sharenet-main`

## Project Structure
- `backend/`: Express, MongoDB, Socket.IO, and Twilio backend
- `softwareproject/`: React/Vite frontend
- `README.md`: project documentation

## Installed Dependencies
Dependencies have already been installed in both projects:

```bash
cd /Users/tanveersingh/Downloads/sharenet-main/backend
npm install
```

```bash
cd /Users/tanveersingh/Downloads/sharenet-main/softwareproject
npm install
```

## Frontend Status
The frontend starts successfully with:

```bash
cd /Users/tanveersingh/Downloads/sharenet-main/softwareproject
npm run dev
```

It runs at:

```text
http://localhost:5173/
```

The frontend currently hardcodes the deployed Railway backend URL:

```text
https://sharenet-production.up.railway.app
```

Therefore, the local frontend currently uses the hosted backend for API and Socket.IO requests unless those URLs are changed to localhost.

## Backend Start Command
Start the backend from the backend directory, not the repository root:

```bash
cd /Users/tanveersingh/Downloads/sharenet-main/backend
npm run dev
```

The backend should use port `5000` if `PORT=5000` is configured. Otherwise its code defaults to port `8080`.

## Current Backend Error
The backend currently crashes with:

```text
[dotenv] injecting env (0) from .env
ACCOUNT: undefined
KEY SID: undefined
KEY SECRET LENGTH: undefined
SID: undefined
Error: The `uri` parameter to `openUri()` must be a string, got "undefined".
```

Meaning: `backend/.env` is either missing, empty, saved in the wrong directory, or contains invalid/missing variable names. `MONGO_URI` is not being loaded.

## Required File
Create this file exactly here:

```text
/Users/tanveersingh/Downloads/sharenet-main/backend/.env
```

It must be beside `server.js` and `package.json`.

Required variable names used by the code:

```env
PORT=5000
MONGO_URI=YOUR_REAL_MONGODB_ATLAS_CONNECTION_STRING
JWT_SECRET=YOUR_LOCAL_JWT_SECRET
TWILIO_ACCOUNT_SID=YOUR_REAL_TWILIO_ACCOUNT_SID
TWILIO_API_KEY_SID=YOUR_REAL_TWILIO_API_KEY_SID
TWILIO_API_KEY_SECRET=YOUR_REAL_TWILIO_API_KEY_SECRET
```

Do not use the placeholder values literally. Do not share the `.env` file or commit it to GitHub.

## How to Create `.env` in VS Code
1. Right-click the `backend` folder in the Explorer.
2. Select **New File**.
3. Name it `.env`.
4. Paste the variables above and replace them with real values.
5. Save the file.
6. Restart the backend with `npm run dev` from the `backend` directory.

The `.env` file may not appear in the Explorer because it is a hidden dotfile.

## MongoDB Setup
A real MongoDB Atlas connection is required because `backend/config/db.js` runs:

```js
mongoose.connect(process.env.MONGO_URI)
```

Create a MongoDB Atlas cluster, create a database user, allow the development machine IP under Network Access, and copy the Drivers connection string. Replace the username and password in that string.

If the MongoDB password contains special URL characters, URL-encode the password.

## Twilio Setup
Twilio is used for audio/video call tokens.

1. Create or log into a Twilio account.
2. Copy the Account SID from the Twilio Console.
3. Open API Keys & Tokens.
4. Create a Standard API key.
5. Copy the API Key SID and API Key Secret.
6. Put them in `backend/.env` using the exact names above.

Trial accounts may require phone verification and may restrict calls to verified numbers.

## JWT Secret
A local JWT secret can be generated with:

```bash
openssl rand -base64 32
```

## Important Clarification
Typing lines such as `PORT=5000` directly at the normal shell prompt does not create `backend/.env`. The values must be saved in the file, or exported in the same shell before starting Node.

## Expected Successful Backend Output
After valid environment variables are loaded, expected output is similar to:

```text
MongoDB Connected: ...
API + Signaling Server running on port 5000
```

## Root Package Warning
The repository root has no `dev` script. This command fails from the root:

```bash
npm run dev
```

Use the backend or frontend directory-specific commands instead.

## Recommended Next Troubleshooting Steps
1. Confirm the current terminal directory:

```bash
pwd
```

It must end in `/sharenet-main/backend` before running the backend.

2. Confirm the environment file exists without printing its secrets:

```bash
ls -la .env
```

3. Confirm the file has the expected variable names without sharing its contents publicly.
4. Confirm `MONGO_URI` is a real Atlas URI, not a placeholder.
5. Restart:

```bash
npm run dev
```

6. If the backend starts but the local frontend still contacts Railway, update the hardcoded backend URLs in the frontend or continue using the deployed backend.
