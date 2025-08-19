# AI-OPADS-MODEL

Verzeichnis Notebook: /srv/Model/AI-OPADS-MODEL
Virtual Environment: /srv/Model/venv

Datenbank:

losmodel_ (Benutzer: admin_db)

Service-Datei "voila-model.service" in /etc/systemmd/system/:
```
[Unit]
Description=Voila Model App

[Service]
ExecStart=/srv/Model/venv/bin/voila --port=8877 /srv/Model/AI-OPADS-MODEL/MeinModelNotebook.ipynb --no-browser --enable_nbextensions=True
WorkingDirectory=/srv/Model/AI-OPADS-MODEL
Restart=always
User=www-data
Group=www-data

[Install]
WantedBy=multi-user.target
```

Zusätzliche Nginx-Konfiguration:

```
location /model/ {
    proxy_pass http://localhost:8877/;
    proxy_set_header Host $host;
    proxy_set_header X-Real-IP $remote_addr;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header X-Forwarded-Proto $scheme;
}
```
