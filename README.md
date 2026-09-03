[README.md](https://github.com/user-attachments/files/31777382/README.md)
# NIKESH PRINT HUB
Scan • Upload • Print

A self-service, no-payment printing workflow: customer QR → upload → print settings → server queue → Windows Print Agent → system printer.

## Requirements
- Node.js 18+
- MySQL 8+
- Windows computer with installed printer
- SumatraPDF installed and available as `SumatraPDF.exe` on PATH for the included Windows PDF print command.

## Setup
1. Create/import the database:
   `mysql -u root -p < database/schema.sql`
2. Copy `backend/.env.example` to `backend/.env` and set secure secrets.
3. In `backend/`: `npm install`, then `npm start`.
4. Open `http://localhost:5000`.
5. Configure `print-agent/config.json` with server URL, station ID, printer name and the same agent token as `.env`.
6. In `print-agent/`: `npm install`, then `npm start`.
7. Visit `/admin/login`. Use the username/password from `.env`.
8. Station QR URL example: `http://YOUR-HOST/upload.html?station=PRINT-01`.

## Important Windows printing note
The agent uses Windows PowerShell printer discovery and invokes SumatraPDF for a real print command. Install SumatraPDF and ensure `SumatraPDF.exe` is available on PATH. For unattended production printing, run the agent under a Windows account that can access the intended printer.

## Security
- Allow only PDF/JPEG/PNG uploads
- 25 MB upload limit
- Random server-side file names
- JWT-protected admin routes
- Agent token authentication
- No executable uploads
- Do not commit `.env`
- Put the server behind HTTPS in production and add a reverse proxy/rate limiter.

## Scope
This project intentionally contains no payment, pricing, checkout, amount, wallet, transaction or revenue features.
