# CheatSheet Creator

This repository contains the necessary infrastructure for simplified deployment of the **CheatSheet Creator** using Docker. This application allows you to create, manage, and print dense cheatsheets in A4 format.

The project has been optimized to run on both **x64 (PC/Servers)** machines and **ARM64 (Orange Pi, Raspberry Pi)** architectures, making it ideal for self-hosting in homelabs.

## Prerequisites

Before getting started, ensure you have installed:
* [Docker](https://docs.docker.com/get-docker/)
* [Docker Compose](https://docs.docker.com/compose/install/)

## Getting Started

1.  **Clone this repository:**
    ```bash
    git clone https://github.com/EliederSousa/cheatsheet-creator-selfhosted.git
    cd cheatsheet-creator-selfhosted
    ```

2.  **Configure environment variables:**
    
    Create the `.env` file from the example:
    ```bash
    cp .env.example .env
    ```
    Edit the `.env` file and fill in the necessary keys (see the [Configuration](#configuration-env) section).

3.  **Start the containers:**
    ```bash
    docker-compose up -d
    ```

The application will be available at:
* **Frontend:** `http://localhost:14000` (or the port defined in the .env file)
* **API:** `http://localhost:14001`

---

## Configuration (.env)

The `.env` file controls the system's behavior. Below are the main variables:

| Variable | Description | Default |
| :--- | :--- | :--- |
| MONGO_ROOT_USER | Default MongoDB user | admin |
| MONGO_ROOT_PASS | Put a strong password here! | mysecretpassword |
| MONGO_DATABASE | MongoDB database name | cheatsheetdb |
| MONGO_PORT | 14002 | MongoDB port |
| API_PORT | API port | 14001 |
| CORS_ALLOWED_ORIGINS | Put a list of domains that can host the frontend | <empty> |
| RATE_LIMIT | Limit the of request/min to the API (must be a positive number) | 100 | 
| FRONTEND_PORT | The frontend port | 14000 |
| VITE_API_SERVER | IP:PORT of API | localhost:14001 |
| VITE_API_KEY | Left blank if you want a read-only instance | mysecretapipassword |

---

## API Limitations

To ensure performance and prevent abuse, the API has the following native restrictions:

1.  **File Size:** The maximum allowed size for uploads (such as icons or JSON attachments) is **2MB**.
2.  **Request Size:** The total payload of each POST request cannot exceed **2MB**.
3.  **Rate Limit:** By default, the API limits requests to **100 requests/minute** per user (adjustable via `RATE_LIMIT`).
4.  **Logs:** Logs are configured to display the execution thread, facilitating concurrency debugging on limited hardware.

---

## Project Structure

* **Frontend (Vue.js):** Reactive interface for editing and visualization.
* **Backend (Spring Boot 3):** REST API managing persistence.
* **Database (MongoDB):** Storage for cheatsheet JSON documents.

## Disclaimer

This software is provided "as is", without warranty of any kind. The author shall not be liable for any claim, damages, or other liability, including but not limited to data loss or hardware failure, arising from the use of this software.

---
Created with **Vue, Spring Boot, and ❤️** by [Elieder Sousa](https://www.linkedin.com/in/eliedersousa/).