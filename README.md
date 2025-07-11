# MERN Stack E-Commerce Website (Clothing Store) with CI/CD Pipeline

A full-stack MERN-based E-Commerce application for a clothing store, featuring product management, user authentication, and fully containerized deployment with Docker and CI/CD automation using Jenkins.

# Features

- Clothing E-Commerce Website  
- User Registration & Login with JWT Authentication  
- Password Hashing with Bcrypt  
- Product Listing & Management  
- Protected Admin Routes (Optional)  
- React.js Frontend + Node.js/Express Backend  
- MongoDB Integration  
- Dockerized Frontend & Backend  
- CI/CD Pipeline with Jenkins  

# Tech Stack

- **Frontend:** React.js  
- **Backend:** Node.js, Express.js  
- **Database:** MongoDB  
- **Authentication:** JWT, Bcrypt  
- **DevOps:** Docker, Jenkins  

## Project Setup

### Prerequisites

- Node.js  
- MongoDB  
- Docker  
- Jenkins  

### Backend Setup

```bash
cd backend
npm install
npm start
```

### Frontend Setup

```bash
cd frontend
npm install
npm start
```

### Docker Setup

- Backend Container:  
  ```bash
  docker build -t ecommerce-backend ./backend
  docker run -p 5000:5000 ecommerce-backend
  ```

- Frontend Container:  
  ```bash
  docker build -t ecommerce-frontend ./frontend
  docker run -p 3000:3000 ecommerce-frontend
  ```

# Jenkins CI/CD Setup

- Configure Jenkins pipeline using the provided `Jenkinsfile`.  
- Set up webhooks for automatic build and deployment on code push.
- also get the live link for ngrok.

# Folder Structure

```
├── backend
├── frontend
├── Jenkinsfile
├── docker-compose.yml (optional)
├── README.md
```


