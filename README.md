# Full Stack Realtime Chat App

A full-stack chat application built with the MERN stack, Socket.IO, and Cloudinary. The project supports authentication, one-to-one realtime messaging, online presence, profile image uploads, and a responsive React frontend.

![Application Screenshot](./frontend/public/screenshot-for-readme.png)

## Overview

This project demonstrates an end-to-end realtime messaging workflow:

- Users can create an account and log in securely
- Authenticated users can browse available contacts
- Users can exchange text and image messages in realtime
- Online/offline presence updates are pushed live with Socket.IO
- Profile photos can be uploaded and stored via Cloudinary

The application is structured as a complete frontend and backend system rather than a backend-only API demo.

## Features

- JWT authentication with `httpOnly` cookies
- Protected backend routes with auth middleware
- One-to-one chat between registered users
- Realtime message delivery using Socket.IO
- Online user presence tracking
- Image attachments in chat
- Profile image upload and update
- Global frontend state management with Zustand
- Theme switching with DaisyUI
- Responsive UI built with React, Tailwind CSS, and Vite

## Tech Stack

### Frontend

- React
- Vite
- Zustand
- React Router
- Axios
- Tailwind CSS
- DaisyUI
- Socket.IO Client

### Backend

- Node.js
- Express
- MongoDB
- Mongoose
- Socket.IO
- JWT
- bcryptjs
- cookie-parser
- Cloudinary

## Architecture

### Frontend

The React frontend lives in `frontend/` and is responsible for:

- Authentication flows
- Route protection and navigation
- Contact list and active chat UI
- Realtime message updates
- Theme persistence

State is managed primarily with Zustand:

- `useAuthStore` handles session state, auth actions, and socket connection
- `useChatStore` handles contacts, active conversation, messages, and live subscriptions
- `useThemeStore` handles theme preference persistence

### Backend

The Express backend lives in `backend/` and is responsible for:

- User authentication and session cookie issuance
- Route protection via JWT verification
- Message persistence in MongoDB
- Profile and message image uploads to Cloudinary
- Realtime events for online presence and new messages

Core API groups:

- `/api/auth`
- `/api/messages`

## Current Scope

This version currently supports direct user-to-user messaging. It does not yet include:

- Group chat rooms
- Message read receipts
- Typing indicators
- Search
- Formal load-testing metrics

## Project Structure

```text
fullstack-chat-app/
├── backend/
│   ├── src/
│   │   ├── controllers/
│   │   ├── lib/
│   │   ├── middleware/
│   │   ├── models/
│   │   └── routes/
├── frontend/
│   ├── public/
│   └── src/
│       ├── components/
│       ├── lib/
│       ├── pages/
│       └── store/
├── package.json
└── README.md
```

## Environment Variables

Create a `.env` file in the `backend/` directory with the following values:

```env
MONGODB_URI=your_mongodb_connection_string
PORT=5001
JWT_SECRET=your_jwt_secret

CLOUDINARY_CLOUD_NAME=your_cloudinary_cloud_name
CLOUDINARY_API_KEY=your_cloudinary_api_key
CLOUDINARY_API_SECRET=your_cloudinary_api_secret

NODE_ENV=development
```

## Installation

Install dependencies for the root project, backend, and frontend:

```bash
npm install
npm install --prefix backend
npm install --prefix frontend
```

## Running the Project

### Start the backend

```bash
npm run dev --prefix backend
```

### Start the frontend

```bash
npm run dev --prefix frontend
```

Frontend development server:

```text
http://localhost:5173
```

Backend API server:

```text
http://localhost:5001
```

## Production Build

Build the frontend and install backend/frontend dependencies:

```bash
npm run build
```

Start the production server:

```bash
npm start
```

## API Summary

### Auth

- `POST /api/auth/signup`
- `POST /api/auth/login`
- `POST /api/auth/logout`
- `GET /api/auth/check`
- `PUT /api/auth/update-profile`

### Messages

- `GET /api/messages/users`
- `GET /api/messages/:id`
- `POST /api/messages/send/:id`

## Realtime Behavior

Socket.IO is used for:

- Broadcasting the current list of online users
- Delivering new messages to connected recipients in realtime

When a user logs in successfully, the frontend opens a socket connection and registers the current user ID. The backend maps each connected user to a socket ID and emits presence updates to all clients.

## Why This Project Matters

This project is useful as a portfolio or interview project because it demonstrates:

- Full MERN application structure
- Authentication and protected routes
- Realtime communication patterns
- Media upload integration
- Client-side and server-side state coordination

## Notes

- The application is fully MERN end to end, not just a backend service
- Messaging is currently one-to-one rather than room-based
- No benchmark or concurrency results are documented in this repository yet
