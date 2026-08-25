# Online Banking with Java, Spring Boot, Angular 2

Developed an Banking website which lets you deposit or withdraw money, schedule an appointment with a banker, view bank statements, transfer money between primary or savings account or with other customer.

Created two separate server:

- User Frontend
- Admin Portal

## User Frontend 

User-Front is a user-facing system and it includes modules such as User Signup/Login, Account, Transfer, Appointment, Transaction and User Profile.

## Admin Portal

It is mainly used by Admin and it involves User Account and Appointment modules. Admin can enable/disable Users, view statements of every Users, confirm an appointment.

## Technologies Used

**Front-end:** Html5/CSS3, JavaScript, TypeScript, JQuery, Bootstrap, Angular 2 and some JS plugins, JSON, Thymeleaf

**Back-end:** Java 8, Spring Boot, Spring Data, Spring Security, Hibernate, MySQL, Maven, Log4j


## DevOps / CI-CD Setup

This project has been containerized and equipped with a full CI/CD pipeline:

### Docker

- **UserFront** (Spring Boot) and **AdminPortal** (Angular, served via nginx) are each built as separate Docker images using multi-stage Dockerfiles (Maven/JDK build stage → lightweight JRE/nginx runtime stage).
- **MySQL 5.7** runs as a containerized service with a healthcheck, persisted via a named volume (`mysql_data`).
- All services are orchestrated with `docker-compose.yml`:
  - `mysql` — database, exposed on port 3306
  - `userfront` — Spring Boot backend, exposed on port 8081
  - `adminportal` — nginx-served Angular frontend, exposed on port 80
  - `jenkins` — CI/CD server, exposed on port 8090

### Jenkins CI/CD

- Jenkins runs in its own Docker container, built from a custom image (`Jenkins.Dockerfile`) that adds the Docker CLI and Docker Compose plugin on top of the official `jenkins/jenkins:lts-jdk17` image.
- The Docker socket (`/var/run/docker.sock`) is mounted into the Jenkins container, allowing Jenkins to build images and manage containers directly on the host.
- The project workspace is bind-mounted into the Jenkins container at `/workspace`.
- Jenkins home (plugins, jobs, credentials) is persisted via the named volume `jenkins_home`.
- Pipeline goal: automated **build → test → Docker image build → deploy** on every push.

### Quick start

```bash
docker compose up -d
```

Then access:
- User Frontend: http://localhost:8081
- Admin Portal: http://localhost
- Jenkins: http://localhost:8090

