# Edlgütl – Website (Contao 5)

Projektwebsite auf Basis von **Contao 5 Managed Edition**.

---

## Erstinstallation auf dem Server

```bash
ssh woidapp@w8.hostingwerk.de
cd ~/html

# Repo klonen
git clone https://github.com/hauge/core.git edlgutl
cd edlgutl
git checkout claude/edlgutl-homepage-contao5-jhn49d

# .env.local mit echten DB-Zugangsdaten anlegen
cp .env .env.local
nano .env.local   # DATABASE_URL und APP_SECRET setzen

# Pakete installieren
composer install --no-dev --optimize-autoloader

# Contao-Datenbank anlegen
php vendor/bin/contao-console contao:migrate

# Cache leeren
php vendor/bin/contao-console cache:clear
```

## Updates einspielen

```bash
cd ~/html/edlgutl
git pull
composer install --no-dev --optimize-autoloader
php vendor/bin/contao-console contao:migrate
php vendor/bin/contao-console cache:clear
```

## Nginx-Konfiguration

Der Nginx-Webroot muss auf `public/` zeigen:

```nginx
root /home/woidapp/html/edlgutl/public;
```

---

## Projektstruktur

```
edlgutl/
├── composer.json        # Abhängigkeiten
├── .env                 # Env-Template (committed)
├── .env.local           # Echte Credentials (NICHT committed)
├── config/              # Symfony-Konfiguration
├── contao/
│   ├── dca/             # Datenbankdefinitionen (Erweiterungen)
│   ├── languages/       # Übersetzungen
│   └── templates/       # Custom Templates (Twig)
├── public/              # Webroot (nginx root)
├── var/                 # Cache & Logs (gitignored)
└── vendor/              # Composer-Pakete (gitignored)
```
