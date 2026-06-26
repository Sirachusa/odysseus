# Odysseus – Project Context for Claude Code

## A projekt lényege
Ez egy self-hosted AI workspace (Odysseus) amelyet egy személyes, 
autonóm AI ökoszisztémává fejlesztünk. A végcél: egy végtelen 
felhasználhatóságú rendszer ahol az egyetlen korlát a hardver kapacitása.
Ha van rá mód és lehetőség, akkor egy magyar projekt, mely Marveen névre hallgat és 
egy autonóm multi-agent rendszer összehangolása és/vagy párhuzamosítása, tájékoztatva a felhasználót 
az esetleges előnyökről és hátrányokról, kapacitás szükségességéről és 
a hozzá tartozó anyagi vonzatokról teljes terjedelmességgel.

## Hardver
- CPU: Intel Core i7-14700F
- RAM: 32GB DDR5
- GPU: NVIDIA GeForce RTX 4070 Ti SUPER 16GB VRAM
- OS: Windows 11 Pro
- WSL2: Ubuntu 24.04 (ez az elsődleges munkakörnyezet)

## Architektúra
- **Odysseus** fut Docker-ben (WSL2-ben), elérhető: http://localhost:7000
- **Docker Compose** stack: Odysseus + ChromaDB + SearXNG + ntfy
- **GPU overlay**: docker-compose.yml:docker/gpu.nvidia.yml (NVIDIA Container 
  Toolkit telepítve, GPU passthrough működik)
- **Ollama** fut WSL2-ben natívan, OLLAMA_HOST=0.0.0.0:11434 konfiguráción
- **Repo helye**: /home/enterprise/odysseus/

## Telepített Ollama modellek
- gemma3:12b → Default Chat (magyar nyelvű kommunikációhoz optimalizálva)
- deepseek-r1:14b → Deep Research / reasoning
- qwen2.5:14b → Utility model (háttérfeladatok)
- mistral:7b → Tartalék / kisebb feladatok

## AI Defaults konfiguráció
- Default Chat: gemma3:12b
- Research Model: deepseek-r1:14b
- Utility Model: qwen2.5:14b
- Vision: Auto-detect
- Provider endpoint: http://host.docker.internal:11434/v1

## TNG (Star Trek: The Next Generation) presetek
A rendszer 5 karakteralapú presettel rendelkezik amelyek személyiséget 
adnak az ágenseknek:
- **Picard** – főasszisztens, diplomáciai, bölcs döntéshozó
- **Data** – analitikus, precíz, kódelemzés
- **Troi** – összefoglalás, értelmezés, empátia
- **Geordi** – technikai problémamegoldás, engineering
- **Guinan** – brainstorming, kreatív ötletelés, széles perspektíva

A presetek system promptjai tartalmazzák:
- Karaktertartás utasítást (never break character)
- Nyelvi utasítást (respond in the same language as the user)

## Aktuális beállítások státusza
- Search: Results=10, Extract Parallel=6, Max Tokens=32768
- Agent Tools: Max steps=50, minden beépített tool engedélyezve
- Open Signup: KI van kapcsolva (biztonság)
- Playwright MCP: telepítendő (böngésző tool az ágenseknek)
- Integrations: még nincs konfigurálva (email, ntfy, webhookok)

## Tervezett fejlesztések
1. **Cloudflare Tunnel** – külső elérés egy 11 éves lány számára aki 
   tableten keresztül szeretné használni tanulásra (korlátozott, 
   kontrollált hozzáférés szükséges)
2. **Gyerekbarát preset** – korosztályos tartalomszűrés, admin 
   felügyelet lehetőségével
3. **MCP szerverek** – Playwright (böngésző), DeepL (fordítás), 
   GitHub, fájlrendszer, stb.
4. **Email integráció** – IMAP/SMTP
5. **Automatikus indítás** – WSL2 + Docker Compose bootkor indul
6. **Ntfy értesítések** – push notifikációk

## Fontos fájlok
- `.env` – fő konfiguráció (COMPOSE_FILE, APP_PORT, AUTH_ENABLED stb.)
- `docker-compose.yml` – alap stack
- `docker/gpu.nvidia.yml` – NVIDIA GPU overlay
- `data/` – minden user adat (presets.json, app.db, memory.json stb.)
- `config/searxng/` – SearXNG konfiguráció

## Amit Claude Code tehet ebben a projektben
- .env és config fájlok módosítása
- Docker Compose fájlok szerkesztése
- Shell parancsok futtatása (docker compose, ollama, systemctl)
- Preset system promptok finomhangolása
- Új MCP szerverek konfigurálása
- Dokumentáció és CLAUDE.md karbantartása
- WSL2 systemd service fájlok létrehozása

## Amit NE csináljon Claude Code
- Ne töröljön adatokat a data/ könyvtárból
- Ne változtassa meg az AUTH_ENABLED=true beállítást
- Ne tegyen publikusan elérhetővé semmilyen portot az APP_BIND módosítása nélkül
- Ne commitoljon .env fájlt vagy API kulcsokat a git repóba
- Ne döntsön egyedül komolyabb kérdésekben vagy drasztikus változtatások esetén
- Az minimális kockázattal járó változtatások kivételével mindig kérjen felhasználó jóváhagyást.

## Munkastílus
- A felhasználó magyarul kommunikál
- Lépésről lépésre haladjunk, minden változtatás előtt magyarázat
- Ha valamit nem lehet visszacsinálni, kérjen megerősítést
- Előnyben részesítjük a minimális, célzott változtatásokat
- Előnyben részesítjük az előre látó, pozitív kritikákat, továbbá az építő jellegű hozzászólásokat
