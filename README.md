### DevOps Semester 2 - Docker Project

This is an educational project for the DevOps semester 2 course. The project involves creating dockerfiles for backend and frontend of a web application.

## Running the Project
1. Clone the repository
2. Navigate to the project directory
3. Run `docker-compose up` to start the containers
4. Access the application at `http://localhost`

## Base Docker Images used
- `alpine:3.22` for the backend  
- `nginxinc/nginx-unprivileged` for the frontend  
Both images create containers with non-root users  
Both images have healthchecks  
