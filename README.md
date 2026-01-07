# 🛡️ Gestione Wireguard da remoto tramite bot telegram

  ![Wireguard](https://img.shields.io/badge/wireguard-%2388171A.svg?style=for-the-badge&logo=wireguard&logoColor=white)
  ![Python](https://img.shields.io/badge/python-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54)
  ![Telegram](https://img.shields.io/badge/Telegram-2CA5E0?style=for-the-badge&logo=telegram&logoColor=white)
  
## Cos'è Wireguard
Wireguard è un protocollo VPN facilmente configurabile all'interno del tuo home lab o sul tuo luogo di lavoro e permette di creare un tunnel sicuro tra il tuo dispositivo e la connessione di destinazione.
Personalmente, ho configurato Wireguard sul mio Virtual Environment seguendo la guida di MorroLinux. 

<p align="center">
  Ecco il video:<br>
  <a href="https://www.youtube.com/watch?v=Ay1guniS3rc">
    <img src="https://img.shields.io/badge/YouTube-%23FF0000.svg?style=for-the-badge&logo=YouTube&logoColor=white" alt="Guarda il video" width="300">
  </a>
</p>

## Come funziona Wireguard
### Cosa fa un client Wireguard
Una volta configurato e attivato, un client Wireguard compie le seguenti operazioni.
- se ho un IP dinamico, WG chiede al dominio fornito dal mio servizio DDNS di ottenere l'IP di destinazione (con IP statico punto direttamente a quello)
- una volta ottenuto l'IP, Wireguard si collega alla destinazione sulla porta 51820. (Se l'IP è 100.100.100.100, WG si collega a 100.100.100.100:51820)
- il router (con port forwarding configurato), vede la chiamata sulla porta 51820 e la reindirizza al server Wireguard (la macchina su cui sta girando WG)

### Cosa fa il server Wireguard
- Quando Wireguard riceve una richiesta, controlla le chiavi e se è tutto a posto accetta la connessione. In caso di chiavi errate, lascia morire la richiesta senza nemmeno dare risposta (ecco perché è **stealth**).


## Aspetti di sicurezza
Wireguard garantisce un tunnel sicuro e protetto, tuttavia in questa configurazione è necessario mantenere una porta aperta sul router.
Questo non è un problema perché, come detto sopra, è impossibile ottenere l'accesso senza le chiavi corrette.
Tuttavia, la porta aperta può essere comunque un "fastidio" per i più paranoici.
Per ridurre l'esposizione del server o semplicemente avere un maggiore controllo, è possibile configurare un bot telegram. Oltre a configurare accensione e spegnimento, una volta configurato sarà possibile implementare altre funzioni come le notifiche ogni qual volta viene stabilita una nuova connessione.


## Contenuti
Nei file della repo sarà possibile trovare:
- impostazione del container Python dove inserire lo script di collegamento con telegram e le relative librerie
- script con il codice
- guida alla configurazione del bot e dell'attivazione in background del processo.


