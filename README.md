#FOODIES Application

## Table of Contents
- [Features](#features)
- [Technology Stack](#technology-stack)
- [Getting Started](#getting-started)
  - [Prerequisites](#prerequisites)
  - [Installation](#installation)
- [Docker Compose Configuration](#docker-compose-configuration)
- [CI/CD](#cicd)

## Features

- **TypeScript**: Strong typing for safer and more manageable code
- **Advanced Authentication**: Login, signup, logout, 6-digit token-based verification, and password recovery
- **Role-Based Accounts**: Secure management of different user roles (Admin, User)
- **Restaurant Management**: Add, edit, and delete restaurants (Admin functionality)
- **Menu Management**: Create and manage menu items for restaurants
- **Order System**: Users can place orders, and admins can manage them
- **Stripe Integration**: Secure payment processing with Stripe, including webhook support
- **Responsive UI**: Built with ShadCN UI & Tailwind CSS for a modern, responsive design
- **State Management**: Utilizes Zustand for efficient state management
- **Form Validation**: Implements Zod for robust schema validation and error handling
- **Email Integration**: Uses Mailtrap for efficient email sending and testing
- **Search Functionality**: Advanced searching capabilities for restaurants and menu items
- **Loading Skeletons**: Enhances user experience with elegant loading states

## Technology Stack

- **Frontend**: React with TypeScript, Vite
- **Backend**: Node.js, Express.js with TypeScript
- **Database**: MongoDB
- **State Management**: Zustand
- **Styling**: Tailwind CSS, ShadCN UI
- **Form Validation**: Zod
- **Authentication**: JWT, 6-digit token verification
- **Payment Processing**: Stripe
- **Email Service**: Mailtrap
- **Deployment**: Docker, Render

## Getting Started

### Prerequisites

- Node.js (v18 or later)
- Docker and Docker Compose
- MongoDB
- Stripe account for payment processing
- Mailtrap account for email testing

### Installation

1. Clone the repository:
   ```
   git clone https://github.com/AshFire1/Food-App-With-CI.git
   ```

2. Navigate to the project directory:
   ```
   cd Food-App-With-CI
   ```

3. Set up environment variables:
   - Create a `.env` file in the `server` directory based on `.env.example`
   - Set up necessary environment variables for both client and server

4. Build and run the Docker containers:
   ```
   docker-compose up --build
   ```

The application should now be running at:
- Frontend: http://localhost:5173
- Backend: http://localhost:3000

## Docker Compose Configuration

```yaml
version: '3.8'

services:
  server:
    dns:
      - 8.8.8.8
      - 8.8.4.4
    build: ./server
    ports:
      - "3000:3000"
    env_file:
      - ./server/.env
    environment:
      - NODE_ENV=production
    depends_on:
      - mongodb

  client:
    build: ./client
    ports:
      - "5173:5173"
    depends_on:
      - server

  mongodb:
    image: mongo:latest
    ports:
      - "27017:27017"
    volumes:
      - mongodb_data:/data/db

volumes:
  mongodb_data:
```

## CI/CD

This project includes a basic CI pipeline using GitHub Actions. The pipeline:

- Installs dependencies for both client and server
- Builds the client application
- Starts both client and server in development mode
- Performs health checks to ensure both are running correctly

To use the CI pipeline, ensure your GitHub repository is connected and the necessary secrets are set up in your GitHub repository settings.

