<div align="center">
  <h1>🛒 E-commerce API — Software Architecture</h1>
  <p>Practical project for the <b>Software Architecture</b> course — UniSatc</p>
</div>

---

## 📚 About the Project
This repository contains the development and evolution of a **REST API built with NestJS** for an e-commerce system, delivered in two iterations.  
The main goal was to apply **architecture concepts**, **scalability**, and **resilience**, with hands-on **performance testing**.

---

## 🚀 Tech Stack
<div align="center">

<a href="https://skillicons.dev">
  <img src="https://skillicons.dev/icons?i=nodejs,nest,ts,redis,postgres,github" alt="Skills" />
</a>

<br/><br/>

<img src="https://img.shields.io/badge/Artillery-000000?style=for-the-badge&logo=artillery&logoColor=white" alt="Artillery">
<img src="https://img.shields.io/badge/Postman-FF6C37?style=for-the-badge&logo=postman&logoColor=white" alt="Postman">

</div>

---

## 📌 API Structure
### Main Endpoints
- **GET `/products`** → List all products (with pagination support).  
- **GET `/products/:id`** → Get details of a specific product.  
- **POST `/cart/add`** → Add an item to the cart (with artificial delay to simulate heavy processing).  
- **GET `/cart/:id`** → Retrieve a cart and its items.  
- **PUT `/cart/:id/items/:productId`** → Update quantity of a cart item.  
- **DELETE `/cart/:id/items/:productId`** → Remove an item from the cart.  

---

# 📦 Delivery 1 — Initial Implementation
### ✔️ Goals
- Implement a shopping cart service (basic CRUD).  
- Expose REST endpoints for the cart.  
- Use in-memory mock products.  
- Manual testing via Postman.  

### 🔨 What was done
- Created `Cart` and `CartItem` models (`model/`).  
- Implemented cart business logic (`CarMarketService`).  
- Created REST controller (`AppController`).  
- Tested adding, updating, removing, and retrieving items.  

---

# ⚡ Delivery 2 — Scalability and Resilience
### ✔️ Goals
- Evolve the API applying **performance** and **resilience** techniques.  
- Add artificial delay in `POST /cart/add` to simulate slow processing.  
- Run **load tests** with Artillery.  
- Implement **Redis cache** for product optimization.  
- Add **timeout** for cart service.  
- *(Optional)* Implement circuit breaker for repeated failures.  

### 🔨 What was done
1. **Load simulation**  
   - Added `setTimeout` in `/cart/add`.  
   - Ran load tests with **Artillery** (latency, RPS, error tracking).  

2. **Redis Cache**  
   - Configured `CacheModule` in `app.module.ts`.  
   - Created `CacheService` with `set`, `get`, `del`.  
   - Applied **Cache-Aside pattern** in `GET /products/:id`.  
   - Redis running locally via Docker.  

3. **Timeout & Resilience**  
   - Timeout applied in `POST /cart/add`.  
   - *(Optional)* Circuit breaker for failing requests.  

4. **New Load Tests**  
   - Compared performance **before and after cache**.  
   - Observed significant latency reduction.  

---

## 📊 Results
- **Before cache:**  
  - Higher latency (every request goes directly to "database").  
  - CPU and I/O usage increased under load.  

- **After cache (Redis):**  
  - Much lower latency (responses served from cache).  
  - Better requests-per-second (RPS).  
  - More stable under high load.  

---

## 🏫 Course Info
- **Course:** Software Architecture  
- **Institution:** UniSatc  


