# Tour de App - Vue + Express boiler plate

Šablona pro vývoj aplikace v soutěži Tour de App společně s frontendovou částí ve frameworku [Vue](https://vuejs.org/), a backendovou částí v [Express](https://expressjs.com/).

## Prvotní nastavení

V složkách pro frontend a backend jsou `.env.example` soubory, které je potřeba přejmenovat na `.env` a upravit hodnoty dle potřeby.

Pro produkční vývoj je potřeba nastavit `VITE_API_URL` na URL API serveru v souboru `tourdeapp.yaml` na URL kterou najdete na hlavní stránce Vašeho projektu na [tourde.cloud](https://tourde.cloud/).

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

2. **Frontend**: V adresáři `apps/web` přejmenujte soubor `.env.example` na `.env`:
   ```bash
   cd ../web
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

Jak se aplikace spustí na [tourde.cloud](https://tourde.cloud/) je definováno v souboru `tourdeapp.yaml` v kořenovém adresáři tohoto repozitáře. V tomto boiler plate jsou předpřipravené služby:
```
- caddy (reverse proxy pro frontend a backend) - stará se o to aby dotazy na Vaší aplikaci byly směrovány na správné místo (tj. /* na frontend a /api/* na backend)
- web (frontend aplikace)
- server (backend aplikace)
- mysql (MySQL databáze)
```

> [!WARNING]
> Databáze není perzistentní, data se z ní po nahrání nové verze aplikace ztratí.

> [!NOTE]
> Reverse proxy je defaultně nastaven tak, že dotazy na `/*` jdou na frontend a `/api/*` pokud by jste chtěli api mít na jiné adresy je nutné změnit soubor `Caddyfile` v adresáři `apps/caddy`.

Co může `tourdeapp.yaml` obsahovat je napsáno v [kde??]().

Do Tour de Cloud se aplikace nahrávají přes [GitHub action](https://github.com/Student-Cyber-Games/upload-app?tab=readme-ov-file), pro nahrání je potřeba zadat **TDC_TOKEN**:
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

Jak odevzdat svojí aplikaci můžete najít v našich [kde??]()

