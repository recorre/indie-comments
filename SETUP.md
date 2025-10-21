# Indie Comments v0.3 Setup Guide

## Prerequisites

- Node.js (version 14 or higher)
- NoCodeBackend API key (from your NoCodeBackend dashboard)

## Installation Steps

1. Install dependencies:
   ```bash
   npm install
   ```

2. Create a `.env` file by copying the example:
   ```bash
   cp .env.example .env
   ```

3. Edit the `.env` file and add your NoCodeBackend API key:
   ```env
   NOCODEBACKEND_API_KEY=your_actual_api_key_here
   ```

4. Start the server:
   ```bash
   npm start
   ```
   
   Or for development with auto-restart:
   ```bash
   npm run dev  # requires nodemon: npm install -g nodemon
   ```

## How It Works

The application uses a backend proxy to securely communicate with NoCodeBackend:

1. The admin panel (frontend) makes requests to `/api/proxy` on your local server
2. The backend server adds the required API key and headers
3. The backend forwards the request to NoCodeBackend
4. The response is relayed back to the frontend

This keeps your API key secure since it's only stored on the server.

## Security Notes

- Never commit your `.env` file to version control
- The widget (`widget/indie_comments.js`) runs on external sites and thus cannot use the proxy
- For production deployment, ensure your server is properly secured
- Use HTTPS in production

## Configuration

- Default port: 4130 (can be changed in `.env`)
- API proxy endpoint: `/api/proxy`
- Admin panel: accessible at `/painel`