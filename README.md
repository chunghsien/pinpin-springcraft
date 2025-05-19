## 🎯 Spring Boot 全方位學習課表

### ⏰ **每日時間建議**

| 模式 | 每日時間   | 完成週期 | 適合族群        |
| -- | ------ | ---- | ----------- |
| 輕量 | 1～2 小時 | 12 週 | 上班族 / 繁忙學習者 |
| 標準 | 3～4 小時 | 6 週  | 學生 / 穩定學習者  |
| 強化 | 6 小時以上 | 4 週  | 全職學習者 / 轉職者 |

> 建議平日輕量、週末補強，依自身狀況調整。

---

# 🚀 Spring Boot API Mastery (PostgreSQL + Redis + JWT)

打造一套實戰級的 Spring Boot API 系統，涵蓋資料庫操作、認證授權、快取優化、Docker 化部署，學習最接近生產環境的開發技能。

---

## 📅 **專案 Milestone 設定**

### 🗂️ Milestone 1：專案初始化與環境建置

* 完成基本開發環境配置與技術選型。

### 🗂️ Milestone 2：認證機制與基本 CRUD 開發

* 實現 JWT 登入註冊與基本資料操作 API。

### 🗂️ Milestone 3：產品模組與 Redis 快取實作

* 完成產品模組 API，整合 Redis 快取與壓力測試。

### 🗂️ Milestone 4：測試與部署

* 撰寫單元測試、整合自動化部署流程與生產環境驗證。

---

## 📚 功能總覽

* ✅ Spring Boot 3.x 開發 RESTful API
* ✅ Spring Data JPA 整合 PostgreSQL 最新版
* ✅ Spring Security + JWT 認證
* ✅ Spring Data Redis 快取機制
* ✅ Swagger / OpenAPI 文件
* ✅ Docker + Docker Compose 一鍵啟動環境
* ✅ 單元測試 + Mock 測試

---

## ⚙️ 開發環境準備

### 1️⃣ 安裝必要工具

* JDK 17+
* Docker & Docker Compose
* Git
* Postman (API 測試工具)

### 2️⃣ 使用 Spring Initializr 建立專案

👉 [點此前往 Spring Initializr](https://start.spring.io/)

* Project: Maven / Gradle
* Language: Java
* Spring Boot: 3.x
* Dependencies:

  * Spring Web
  * Spring Data JPA
  * PostgreSQL Driver
  * Spring Security
  * Spring Data Redis
  * Lombok
  * Spring Boot Validation

---

## 🚀 快速啟動

```bash
# 1. Clone 專案
git clone https://github.com/chunghsien/pinpin-springcraft.git
cd pinpin-springcraft

# 2. 啟動 PostgreSQL + Redis + App
docker-compose up --build

# 3. 測試 API
http://localhost:8080/swagger-ui.html
```

> 📌 如需自訂環境變數，請參考 `.env.example` 檔案建立 `.env`。

---

## 📖 API 認證流程

1. **登入取得 Token**

```http
POST /api/auth/login
Body: { "username": "admin", "password": "password" }
```

2. **攜帶 JWT Token 呼叫 API**

```http
GET /api/products
Headers: Authorization: Bearer <Your_JWT_Token>
```

---

## 📦 Docker Compose 環境

```yaml
version: '3'
services:
  db:
    image: postgres:latest
    environment:
      POSTGRES_USER: root
      POSTGRES_PASSWORD: root
      POSTGRES_DB: ecommerce
    ports:
      - "5432:5432"
    volumes:
      - db_data:/var/lib/postgresql/data
    healthcheck:
      test: ["CMD", "pg_isready", "-U", "root"]
      interval: 30s
      timeout: 10s
      retries: 5

  redis:
    image: redis:latest
    ports:
      - "6379:6379"
    healthcheck:
      test: ["CMD", "redis-cli", "ping"]
      interval: 30s
      timeout: 10s
      retries: 5

  app:
    build: .
    ports:
      - "8080:8080"
    depends_on:
      - db
      - redis

volumes:
  db_data:
```

---

## 🧩 Redis 快取使用範例

```java
@Cacheable(value = "products", key = "#category")
public List<Product> getProductsByCategory(String category) {
    return productRepository.findByCategory(category);
}

@CacheEvict(value = "products", key = "#category")
public void invalidateProductCache(String category) {
    // 快取清除邏輯
}
```

---

## 📚 學習資源

* [Spring 官方教學](https://spring.io/guides)
* [Spring Initializr](https://start.spring.io/)
* YouTube：Amigoscode / Telusko
* 書籍：《Spring in Action》第五版
* 範例專案：[GitHub - Spring Boot API Mastery](https://github.com/chunghsien/pinpin-springcraft)

---

> 持續更新中，歡迎 Star ⭐ 與 Fork 🔥！

---
