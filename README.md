﻿# document_micro-services

---

### Running Microservices with Gateway

#### 1. Start Microservices

Navigate to the directory of each microservice (e.g., auth, signature, document).

```bash
python app.py
```

Repeat this process for each microservice, ensuring they are running on different ports.

#### 2. Run the Gateway

Navigate to the directory of the gateway service.

```bash
python app.py
```

The gateway will start running and will proxy requests to the microservices.

#### 3. Access Services through the Gateway

Once the gateway is running, you can access the services through the gateway's URL.

For example, if the gateway is running on `http://localhost:5000`, you can access the services using routes defined in the gateway (e.g., `http://localhost:5000/auth/login`, `http://localhost:5000/artifact/upload_artifact`, etc.).

The gateway will forward the requests to the appropriate microservice based on the route.

---

                                +-----------------------+
                                |      Gateway          |
                                |     (Flask App)       |
                                +-----------+-----------+
                                            |
                            +---------------+----------------+
                            |                                |
              +-------------v-------------+    +-------------v--------------+
              |        Auth Service       |    |      Signature Service     |
              |    (Flask App with DB)    |    |   (Flask App with DB)      |
              +-------------+-------------+    +-------------+--------------+
                            |                                |
                            +-----------+      +-------------v--------------+
                                        |      |      Document Service      |
                              +---------v------+    (Flask App with DB)     |
                              |       DB (SQLite)      +-----------+--------+
                              |  (Shared Database)     |
                              +------------------------+
