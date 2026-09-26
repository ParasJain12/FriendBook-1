# 📸 FriendBook

A full-stack **social networking web app** (an Instagram-style clone) built with **Spring Boot**, where users can sign up, post photos, like & comment, follow/unfollow people, send friend requests, and search for other users — complete with Docker, Kubernetes, and CI/CD pipelines for deployment.

---

## 📌 What is this project?

**FriendBook** is a mini social media platform inspired by Instagram. Users can create an account, build a profile, share posts with images, interact with other users' content (likes & comments), and grow their network through **follow** and **friend request** systems. The project isn't just an app — it also comes fully "production-ready" with a **Dockerfile, docker-compose setup, Kubernetes manifests, and Jenkins/Azure CI/CD pipelines**, making it a great end-to-end DevOps + full-stack showcase.

---

## ✨ Features / Functionality

### 👤 Authentication & Profile
- 📝 User **signup** with **Google reCAPTCHA** bot protection
- 🔐 Secure **login/logout** via Spring Security (BCrypt password hashing)
- 🖼️ Upload & update **profile picture** and profile details
- 🔍 **Search users** by username

### 📷 Posts
- 📤 **Create posts** with image/media uploads
- ✏️ **Edit** and 🗑️ **delete** your own posts
- 🧵 View a personalized **feed** of posts

### ❤️ Engagement
- 👍 **Like / unlike** posts, with live like counts
- 💬 **Comment** on posts and delete your own comments
- 🔔 **Notifications** for social activity

### 🤝 Social Graph
- ➕ **Follow / unfollow** other users
- 👥 View a user's **followers** and **following** lists
- 🤝 Send, **accept**, or **decline friend requests**
- 🔁 **Follow-back** shortcut from incoming requests

### ☁️ DevOps / Deployment Ready
- 🐳 Multi-stage **Dockerfile** (Maven build → lightweight JRE runtime image)
- 🧩 **docker-compose.yml** to spin up the app + MySQL together
- ☸️ **Kubernetes manifests** (Deployment, Service, PVC, HPA, Ingress, Secrets, Namespace) for cluster deployment
- 🔁 **Jenkins pipeline** & **Azure Pipelines** config for CI/CD (build → Docker image → push)

---

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| **Language** | ☕ Java 21 |
| **Framework** | 🍃 Spring Boot 3.5.4 |
| **Web Layer** | Spring MVC (`spring-boot-starter-web`) + REST controllers |
| **Templating** | 🌿 Thymeleaf (+ Spring Security integration) |
| **Security** | 🔐 Spring Security + BCrypt, Google reCAPTCHA |
| **Data Access** | 🗄️ Spring Data JPA / Hibernate |
| **Database** | 🐬 MySQL (H2 used for tests) |
| **Validation & Mapping** | Spring Validation, ModelMapper, DTOs |
| **Boilerplate Reduction** | 🧬 Lombok |
| **Frontend/UI** | HTML, CSS, JavaScript (Thymeleaf views) |
| **Build Tool** | 🏗️ Maven (`mvnw` wrapper included) |
| **Containerization** | 🐳 Docker & Docker Compose |
| **Orchestration** | ☸️ Kubernetes (Deployment, HPA, Ingress, Secrets) |
| **CI/CD** | 🔁 Jenkins Pipeline, Azure Pipelines |
| **Testing** | JUnit + Spring Boot Test + Spring Security Test |

### 📁 Project Structure
```
FriendBook-1/
├── src/main/java/com/friendbook/
│   ├── configuration/    # SecurityConfig, WebConfig, AppConfig, NoCacheFilter
│   ├── controller/       # PageController, PostController, LikeController,
│   │                     #   CommentRestController, FollowController,
│   │                     #   FriendRequestController, SearchController, UserRestController
│   ├── model/            # User, Post, Media, Comment, PostLike, Follow, FriendRequest
│   ├── repository/       # Spring Data JPA repositories
│   ├── service / impl/   # Business logic (Post, User, Comment, Like, Follow, FriendRequest)
│   ├── dto/               # UserDTO
│   ├── utility/           # CaptchaUtility, RecaptchaService, SignupResponse
│   └── exception/         # UserNotFoundException
├── src/main/resources/
│   ├── templates/         # index, login, signup, profile, posts, notifications, about
│   └── application.properties
├── Dockerfile
├── docker-compose.yml
├── k8s-manifest/           # Kubernetes deployment files
├── JenkinsPipeline
└── azure-pipelines.yml
```

---

## 🚀 How to Run

You can run FriendBook either **locally with Maven + MySQL**, or **with Docker Compose** (recommended, since it also spins up MySQL for you).

### ✅ Prerequisites
- ☕ **Java 21 (JDK)**
- 🐬 **MySQL Server** (if running locally without Docker)
- 🐳 **Docker & Docker Compose** (if running via containers)
- 🏗️ Maven (optional — the `mvnw` wrapper is included)

---

### 🅰️ Option 1: Run locally with Maven

**1️⃣ Clone the repository**
```bash
git clone https://github.com/ParasJain12/FriendBook-1.git
cd FriendBook-1
```

**2️⃣ Create the MySQL database**
```sql
CREATE DATABASE friendbook;
```
> Tables are auto-created/updated on startup via `spring.jpa.hibernate.ddl-auto=update`.

**3️⃣ Configure credentials**
Update `src/main/resources/application.properties` (or pass as environment variables) with your DB and reCAPTCHA credentials:
```properties
spring.datasource.url=jdbc:mysql://localhost:3306/friendbook
spring.datasource.username=YOUR_MYSQL_USERNAME
spring.datasource.password=YOUR_MYSQL_PASSWORD

google.recaptcha.secret=YOUR_RECAPTCHA_SECRET_KEY
google.recaptcha.site=YOUR_RECAPTCHA_SITE_KEY
```
> ⚠️ **Security tip:** `docker-compose.yml` currently has sample DB and reCAPTCHA keys committed. Replace them with your own and avoid committing real secrets — use environment variables or a secrets manager instead.

**4️⃣ Run the app**
```bash
# macOS/Linux
./mvnw spring-boot:run

# Windows
mvnw.cmd spring-boot:run
```

**5️⃣ Open the app**
Visit **http://localhost:8090** (the app runs on port `8090` by default). 🎉

---

### 🅱️ Option 2: Run with Docker Compose (app + MySQL together)

**1️⃣ Clone the repository**
```bash
git clone https://github.com/ParasJain12/FriendBook-1.git
cd FriendBook-1
```

**2️⃣ Start everything with one command**
```bash
docker-compose up -d
```
This spins up:
- 🐬 A MySQL 8 container (`friendbook_mysql`)
- 🚀 The FriendBook app container (`friendbook_apps`), waiting for MySQL to be ready before starting

**3️⃣ Open the app**
Visit **http://localhost:8090** 🎉

**4️⃣ Stop everything**
```bash
docker-compose down
```

---

### ☸️ Option 3: Deploy to Kubernetes
Manifests are provided under `k8s-manifest/` (namespace, MySQL deployment + PVC, app deployment, HPA, and Ingress). Apply them in order:
```bash
kubectl apply -f k8s-manifest/namespace.yaml
kubectl apply -f k8s-manifest/mysql-secret.yaml
kubectl apply -f k8s-manifest/mysql-pv-pvc.yaml
kubectl apply -f k8s-manifest/mysql-deployment.yaml
kubectl apply -f k8s-manifest/friendbook-deployment.yaml
kubectl apply -f k8s-manifest/hpa.yaml
```
> Note: `ingress.yaml` and `mysql-service.yaml` are currently empty placeholders in the repo — fill these in with your Ingress/Service definitions before applying.

---

## 📄 License

This project is open source and available under the [MIT License](LICENSE).

---

## 📬 Contact

For any queries, reach out at **parasjain8103@gmail.com** or use the [Contact Us](https://parasjain12.github.io/) page on the website.

---

<p align="center">Made with ❤️ by Paras Jain</p>
