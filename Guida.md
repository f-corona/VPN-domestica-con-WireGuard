### Guida all'installazione dell'ambiente Python e configurazione del Bot Telegram

## Parte 1 - Python
Installazione python
<br> `apt update && apt install python3 python3-venv python3-pip -y`

Creazione cartella di lavoro
<br> `mkdir -p /opt/wg-telegram-bot`
<br> `cd /opt/wg-telegram-bot`

Creiamo il file bot.py e copiamo il codice all'interno del file bot.py
<br> `nano /opt/wg-telegram-bot/bot.py`
<br> Chiudiamo e salviamo con CTRL+O, invio, CTRL+X

Avviamo l'ambiente virtuale
<br> `python3 -m venv venv`
<br> `source venv/bin/activate`

Installiamo la libreria necessaria a collegarci con telegram
<br> `pip install python-telegram-bot`

## Parte 2 - Telegram
<br>Cerchiamo `@BotFather` e inviamo `/newbot`
<br>Una volta creato, recuperiamo l'API Token e andiamolo a inserire nel campo dedicato nel file bot.py
<br>Cerchiamo `@userinfobot` su Telegram o altri strumenti per recuperare il proprio ID utente. Anche questo va inserito nell'opportuno campo nel codice.


## Parte 3 - Configurazione del servizio
Da linea di comando, esegui `nano /etc/systemd/system/wg-telegram-bot.service` e incolla il seguente codice:
```
[Unit]
Description=WireGuard Telegram Bot
After=network.target

[Service]
User=root
WorkingDirectory=/opt/wg-telegram-bot
ExecStart=/opt/wg-telegram-bot/venv/bin/python3 /opt/wg-telegram-bot/bot.py
Restart=always

[Install]
WantedBy=multi-user.target
```
In questo modo istruiamo la nostra macchina ad eseguire all'avvio l'ambiente python ogni volta che accendiamo la macchina su cui gira WG.

Una volta salvato, eseguiamo i seguenti comandi:
<br> `systemctl daemon-reload`  - ricarica la configurazione di systemd
<br> `systemctl enable wg-telegram-bot`  - imposta l'avvio automatico al boot
<br> `systemctl start wg-telegram-bot`  - avvia il bot immediatamente
<br> `systemctl status wg-telegram-bot`  - controlla che sia tutto ok

Una volta fatto tutto questo, potete iniziare a inviare messaggi al vostro bot e testare.
<br> I comandi impostati sono:
<br> `/start`
<br> `/wg_on`
<br> `/wg_off`
