# **Industrial Device & Location Management REST API (C++ / SQLite / Docker)**

A high-performance **C++17 REST API server** for managing **industrial devices and locations**, built using the **served** HTTP framework and **SQLite**.
The API supports full CRUD operations, filtering, and is documented using **OpenAPI/Swagger**.
This project includes **CMake** and **Docker** for seamless building and deployment.

---

## 📌 Features

* **Modern C++17 REST API**
* **Device & Location CRUD**
* **SQLite backend with prepared statements**
* **OpenAPI/Swagger documentation**
* **Docker-ready**
* **Clear modular architecture**
* **Lightweight served HTTP engine**

---

## 🏗️ Architecture Overview

```
rest-API-master/
│
├── docs/
│   ├── device-api.yaml        # OpenAPI specification
│   └── Database.md            # Database schema documentation
│
├── src/
│   ├── main.cpp               # Application entry point
│   ├── server/
│   │   ├── server_manager.hpp
│   │   └── server_manager.cpp
│   ├── handlers/              # Business logic for endpoints
│   ├── database/
│   │   ├── database_manager.hpp
│   │   └── database_manager.cpp
│   └── utilities/             # Config helpers, constants, utils
│
├── Dockerfile                 # Build container
├── CMakeLists.txt             # Build configuration
└── README.md
```

---

## ⚙️ Prerequisites

Install the following:

* **CMake ≥ 3.10**
* **GCC/Clang with C++17 support**
* **SQLite3**
* **served library**
* **Docker (optional)**

### Install served

```bash
git clone https://github.com/meltwater/served.git
cd served
mkdir build && cd build
cmake ..
make -j4
sudo make install
```

---

## 🔧 Building the Project

```bash
mkdir build && cd build
cmake ..
make -j4
```

The compiled binary will be located at:

```
build/bin/device-server
```

---

## ▶️ Running the Server

```bash
./device-server
```

Default host & port:

```
http://localhost:8080
```

Configuration values can be changed in:

```
src/utilities/config.hpp
```

---

## 🗄️ Database

The server uses **SQLite**, automatically creating the database and tables on first run.

To reset the DB:

```bash
rm device_database.db
```

(Or the name configured in your source.)

---

## 📘 API Documentation (OpenAPI)

The complete API spec is located at:

```
docs/device-api.yaml
```

### View via Swagger Editor:

Open:
[https://editor.swagger.io](https://editor.swagger.io)
→ Upload `device-api.yaml`

### Run Swagger UI via Docker:

```bash
docker run -p 8081:8080 \
  -e SWAGGER_JSON=/docs/device-api.yaml \
  -v $(pwd)/docs:/docs swaggerapi/swagger-ui
```

Access Swagger UI at:

```
http://localhost:8081
```

---

## 🔌 Example API Usage

### 1. Get all devices

```bash
curl -X GET http://localhost:8080/devices
```

### 2. Filter devices

```bash
curl -X GET "http://localhost:8080/devices?location=Factory-A&status=active"
```

### 3. Create device

```bash
curl -X POST http://localhost:8080/devices \
  -H "Content-Type: application/json" \
  -d '{"name": "Sensor-01", "type": "temperature", "location_id": 3}'
```

### 4. Delete device

```bash
curl -X DELETE http://localhost:8080/devices/5
```

---

## 🐳 Docker Deployment

### Build image:

```bash
docker build -t device-server .
```

### Run container:

```bash
docker run -p 8080:8080 device-server
```

---

## 🧪 Testing (Recommended Setup)

Add tests using:

* **Catch2** for unit tests
* **Curl/Postman** for endpoint tests
* **Docker** for integration testing

Example:

```bash
ctest --output-on-failure
```

---

## 🤝 Contributing

1. Fork the project
2. Create a branch
3. Commit changes
4. Open a Pull Request

Please follow modern C++17 standards and add documentation where needed.

---

## 📄 License

This project uses the license provided in the repository (or you may add one such as MIT/Apache-2.0).

