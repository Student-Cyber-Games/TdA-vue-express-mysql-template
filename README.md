# Tour de App - Vue + Express Boilerplate

> **Note:** Czech version is available below / Česká verze je k dispozici níže

A template for developing applications for the Tour de App competition with a frontend in [Vue](https://vuejs.org/) and a backend in [Express](https://expressjs.com/).

## Initial Setup

In the backend directory, there is a `.env.example` file that needs to be renamed to `.env` and the values adjusted as needed.

> [!WARNING]
> If you want to change the database password, you need to change it in the `tourdeapp.yaml` file, `apps/server/.env`, and for local development in the `apps/server/package.json` file.

## Local Development

For local development, you need to run three services: the database, backend, and frontend. Below you'll find detailed step-by-step instructions.

### Step 1: Setting up environment variables

First, you need to set up environment variables:

1. **Backend**: In the `apps/server` directory, rename the `.env.example` file to `.env`:
   ```bash
   cd apps/server
   cp .env.example .env
   ```

### Step 2: Installing dependencies

Install dependencies for both parts of the application:

1. **Backend dependencies**:
   ```bash
   cd apps/server
   npm install
   ```

2. **Frontend dependencies**:
   ```bash
   cd ../web
   npm install
   ```

### Step 3: Starting the MySQL database

Start the database using a Docker container:

```bash
cd apps/server
npm run db
```

The database will run on port **3306**. Wait a few seconds for the database to fully initialize (usually 10-20 seconds).

> [!WARNING]
> The database is not persistent, data will be lost after shutting down the Docker container.

> [!TIP]
> If you need to stop the database, use `docker ps` to view running containers and `docker stop <container-id>` to stop the database container.

### Step 4: Starting the backend server

In a new terminal, start the backend:

```bash
cd apps/server
npm run dev
```

The backend will run on [http://localhost:3000](http://localhost:3000). You should see a message that the server is running and connected to the database.

### Step 5: Starting the frontend application

In another terminal, start the frontend:

```bash
cd apps/web
npm run dev
```

The frontend will run on [http://localhost:3001](http://localhost:3001). Open this address in your browser.

### Verifying everything works

1. **Frontend**: Open [http://localhost:3001](http://localhost:3001) - your application should be displayed
2. **Backend API**: Open [http://localhost:3000/api](http://localhost:3000/api) - you should see a response from the API
3. **Database**: You can connect using a MySQL client to `localhost:3306` with username `root` and password `password`

### Troubleshooting

- **Port already in use**: If any of the ports (3000, 3001, 3306) are already in use, terminate the process using it or change the port in the configuration files
- **Database won't start**: Check that you have Docker installed and running
- **Backend can't connect to database**: Wait for the database to fully initialize (usually takes 10-20 seconds after starting)
- **Node.js is not installed**: Install Node.js from [nodejs.org](https://nodejs.org/) or use a version manager like `nvm` (Linux/MacOS: `curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | bash`, Windows: download from [nvm-windows](https://github.com/coreybutler/nvm-windows))

## Production Setup (how does it run on our servers?)

How the application runs on [tourde.cloud](https://tourde.cloud/) is defined in the `tourdeapp.yaml` file in the root directory of this repository. This boilerplate includes pre-configured services:
```
- caddy (reverse proxy for frontend and backend) - handles routing requests to your application to the correct place (i.e., /* to frontend and /api/* to backend)
- web (frontend application)
- server (backend application)
- mysql (MySQL database)
```

> [!WARNING]
> The database is not persistent, data will be lost after uploading a new version of the application.

> [!NOTE]
> The reverse proxy is set by default so that requests to `/*` go to the frontend and `/api/*` to the backend. If you want to have the API on different addresses, you need to change the `Caddyfile` file in the `apps/caddy` directory.

What `tourdeapp.yaml` can contain is described in [How to deploy an app to Tour de Cloud](https://tourdeapp.com/study-materials/how-to-deploy).

Applications are uploaded to Tour de Cloud via [GitHub action](https://github.com/Student-Cyber-Games/upload-app?tab=readme-ov-file). For uploading, you need to set **TDC_TOKEN**:
- Settings -> (Security) Secrets and variables -> Actions -> New repository secret.
- Name: `TDC_TOKEN` Secret: [your secret generated in [tourde.cloud](https://tourde.cloud/)]


### Prerequisites

#### Windows

- Installed [WSL2 (Windows Subsystem for Linux)](https://learn.microsoft.com/en-us/windows/wsl/install)
- Installed and running [Docker](https://www.docker.com/)
- Installed [Node.js](https://nodejs.org/en/download/)
- Installed [npm](https://www.npmjs.com/get-npm) (usually included with Node.js)

#### Linux / MacOS

- Installed and running [Docker](https://www.docker.com/)
- Installed [Node.js](https://nodejs.org/en/download/)
- Installed [npm](https://www.npmjs.com/get-npm) (usually included with Node.js)

## Submission

How to submit your application can be found in our [How to deploy an app to Tour de Cloud](https://tourdeapp.com/study-materials/how-to-deploy)

---

# Tour de App - Vue + Express Boilerplate

**Česká verze / Czech Version**

Šablona pro vývoj aplikace v soutěži Tour de App společně s frontendovou částí ve frameworku [Vue](https://vuejs.org/), a backendovou částí v [Express](https://expressjs.com/).

## Prvotní nastavení

V složce pro backend je `.env.example` soubor, který je potřeba přejmenovat na `.env` a upravit hodnoty dle potřeby.

> [!WARNING]
> Pokud chcete měnit heslo od databáze, je potřeba ho změnit v souboru `tourdeapp.yaml`, `apps/server/.env` a pro lokální vývoj v souboru `apps/server/package.json`.

## Lokální vývoj

Pro lokální vývoj je potřeba spustit tři služby: databázi, backend a frontend. Níže najdete podrobné instrukce krok za krokem.

### Krok 1: Nastavení environmentálních proměnných

Nejprve je potřeba nastavit environmentální proměnné:

1. **Backend**: V adresáři `apps/server` přejmenujte soubor `.env.example` na `.env`:
   ```bash
   cd apps/server
   cp .env.example .env
   ```

### Krok 2: Instalace závislostí

Nainstalujte závislosti pro obě části aplikace:

1. **Backend závislosti**:
   ```bash
   cd apps/server
   npm install
   ```

2. **Frontend závislosti**:
   ```bash
   cd ../web
   npm install
   ```

### Krok 3: Spuštění MySQL databáze

Databázi spustíte pomocí Docker kontejneru:

```bash
cd apps/server
npm run db
```

Databáze poběží na portu **3306**. Počkejte několik sekund, než se databáze plně inicializuje (obvykle 10-20 sekund).

> [!WARNING]
> Databáze není perzistentní, data se z ní po vypnutí Docker kontejneru ztratí.

> [!TIP]
> Pokud potřebujete databázi zastavit, použijte příkaz `docker ps` pro zobrazení běžících kontejnerů a `docker stop <container-id>` pro zastavení kontejneru s databází.

### Krok 4: Spuštění backend serveru

V novém terminálu spusťte backend:

```bash
cd apps/server
npm run dev
```

Backend poběží na [http://localhost:3000](http://localhost:3000). Měli byste vidět zprávu, že server běží a je připojen k databázi.

### Krok 5: Spuštění frontend aplikace

V dalším terminálu spusťte frontend:

```bash
cd apps/web
npm run dev
```

Frontend poběží na [http://localhost:3001](http://localhost:3001). Otevřete tuto adresu v prohlížeči.

### Ověření, že vše funguje

1. **Frontend**: Otevřete [http://localhost:3001](http://localhost:3001) - měla by se zobrazit vaše aplikace
2. **Backend API**: Otevřete [http://localhost:3000/api](http://localhost:3000/api) - měli byste vidět odpověď z API
3. **Databáze**: Můžete se připojit pomocí MySQL klienta na `localhost:3306` s uživatelským jménem `root` a heslem `password`

### Řešení problémů

- **Port již používán**: Pokud některý z portů (3000, 3001, 3306) je již používán, ukončete proces, který ho používá, nebo změňte port v konfiguračních souborech
- **Databáze se nespustí**: Zkontrolujte, zda máte nainstalovaný a spuštěný Docker
- **Backend se nemůže připojit k databázi**: Počkejte, až se databáze plně inicializuje (obvykle trvá 10-20 sekund po spuštění)
- **Node.js není nainstalován**: Nainstalujte Node.js z [nodejs.org](https://nodejs.org/) nebo použijte správce verzí jako `nvm` (Linux/MacOS: `curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | bash`, Windows: stáhněte z [nvm-windows](https://github.com/coreybutler/nvm-windows))

## Produkční setup (jak se to spouští na našich serverech?)

Jak se aplikace spustí na [tourde.cloud](https://tourde.cloud/) je definováno v souboru `tourdeapp.yaml` v kořenovém adresáři tohoto repozitáře. V tomto boilerplate jsou předpřipravené služby:
```
- caddy (reverse proxy pro frontend a backend) - stará se o to, aby dotazy na Vaší aplikaci byly směrovány na správné místo (tj. /* na frontend a /api/* na backend)
- web (frontend aplikace)
- server (backend aplikace)
- mysql (MySQL databáze)
```

> [!WARNING]
> Databáze není perzistentní, data se z ní po nahrání nové verze aplikace ztratí.

> [!NOTE]
> Reverse proxy je defaultně nastaven tak, že dotazy na `/*` jdou na frontend a `/api/*` na backend. Pokud byste chtěli API mít na jiných adresách, je nutné změnit soubor `Caddyfile` v adresáři `apps/caddy`.

Co může `tourdeapp.yaml` obsahovat je napsáno v [Jak nasadit aplikaci na Tour de Cloud](https://tourdeapp.cz/vzdelavaci-materialy/jak-deploy).

Do Tour de Cloud se aplikace nahrávají přes [GitHub action](https://github.com/Student-Cyber-Games/upload-app?tab=readme-ov-file). Pro nahrání je potřeba zadat **TDC_TOKEN**:
- Settings -> (Security) Secrets and variables -> Actions -> New repository secret.
- Name: `TDC_TOKEN` Secret: [váš secret vygenerovaný v [tourde.cloud](https://tourde.cloud/)]


### Prerekvizity

#### Windows

- Nainstalovaný [WSL2 (Windows Subsystem for Linux)](https://learn.microsoft.com/en-us/windows/wsl/install)
- Nainstalovaný a běžící [Docker](https://www.docker.com/)
- Nainstalovaný [Node.js](https://nodejs.org/en/download/)
- Nainstalovaný [npm](https://www.npmjs.com/get-npm) (bývá součástí Node.js)

#### Linux / MacOS

- Nainstalovaný a běžící [Docker](https://www.docker.com/)
- Nainstalovaný [Node.js](https://nodejs.org/en/download/)
- Nainstalovaný [npm](https://www.npmjs.com/get-npm) (bývá součástí Node.js)

## Odevzdání

Jak odevzdat svoji aplikaci můžete najít v našich [Jak nasadit aplikaci na Tour de Cloud](https://tourdeapp.cz/vzdelavaci-materialy/jak-deploy)
