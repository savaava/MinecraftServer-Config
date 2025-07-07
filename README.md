# Guida alla creazione di un server Minecraft con file `.jar`

## 1. Scelta della versione

Tutti i giocatori devono usare **esattamente la stessa versione** del server per poter connettersi.

È compatibile anche con i client che usano **OptiFine**. <br>
Questo perchè è una mod **solo lato client** per migliorare prestazioni e grafica, ma non modifica il server.

## 2. Download del file `.jar`
Scaricare il file `.jar` della versione scelta da uno dei seguenti siti:

| Tipo di Server   | Sito ufficiale                                                                                  | Plugin/Mod supportati |
|------------------|------------------------------------------------------------------------------------------------|----------------------|
| Vanilla          | [minecraft.net](https://www.minecraft.net/it-it/download/server) *(mostra solo l'ultima versione)*<br>[mcversions.net](https://mcversions.net/) *(per scaricare versioni specifiche)* | ❌ No plugin         |
| PaperMC          | [papermc.io/downloads](https://papermc.io/downloads)                                          | ✅ Plugin            |
| Forge (Modding)  | [files.minecraftforge.net](https://files.minecraftforge.net)                                    | ✅ Mod               |


Rinominare il file `.jar` scaricato in modo che sia facilmente riconoscibile, ad esempio `server-1.21.7.jar`.

## 3. Creazione/Preparazione della cartella del server
- Creare una cartella per il server, ad esempio `MinecraftServer-1.21.7`.
- Inserire il file `.jar` scaricato in questa cartella.
- Creare per comodità un file chiamato ad esempio `StartServer.bat` (Windows):

```bat
@echo off
java -Xms2G -Xmx4G -jar server-1.21.7.jar nogui
pause
```
  - `-Xms2G` → imposta la memoria minima a 2 GB.
  - `-Xmx4G` → imposta la memoria massima a 4 GB.
  - `-jar server-1.21.7.jar` → specifica il file `.jar` del server (il nome deve corrispondere a quello del file scaricato).
  - `nogui` → disabilita l'interfaccia grafica per migliorare le prestazioni.

**Fare doppio clic su `StartServer.bat` avviarerà direttamente il server**.

### 3.1 Requisito di sistema per avviare il server `.jar`
Per avviare il server `.jar`, è necessario avere installato **Java**.  
La versione minima di Java richiesta dipende dalla versione di Minecraft, ma è meglio avere l'ultima versione per evitare problemi di compatibilità.

## 4. Accetta l'EULA
- Avviare il server per la prima volta per generare i file di configurazione.
- Aprire il file `eula.txt` generato e modificare la riga `eula=false` in `eula=true` per accettare i termini di servizio.

## 5. Configurazione del server
- Aprire il file `server.properties` ecco un estratto delle opzioni principali:
```properties
# Impostazioni del server
motd=Benvenuti nel server di Sava!
max-players=10
level-name=SavaWorld
enable-command-block=false
gamemode=survival
difficulty=hard
# Impostazioni di rete
server-port=25565
server-ip=
```

Significato delle opzioni principali:
- `motd` → Messaggio del giorno (visualizzato nella lista dei server)
- `level-name` → Nome del mondo
- `enable-command-block` → Abilita i blocchi comandi (utile per mappe personalizzate)
- `gamemode` → Modalità di gioco predefinita (`survival`, `creative`, `adventure`, `spectator`)
- `difficulty` → Difficoltà del gioco (`peaceful`, `easy`, `normal`, `hard`)

## 6. Port Forwarding
Per far in modo che anche gli amici che non si trovano nella stessa rete locale possano connettersi al server, è necessario configurare il port forwarding sul router sulla porta specifica del server (nel nostro esempio usiamo quella di default: `25565`). <br>
Quindi dovranno connettersi usando l'indirizzo IP pubblico del server, ossia l'indirizzo IP dell'interfaccia WAN del router. <br> 
La porta naturalmente deve essere aperta nel firewall (del router e del PC stesso) e può essere `25565`, oppure qualsiasi altra perchè si effettua in ogni caso il port forwarding sulla porta `25565`.

### 6.1 Aprire la porta 25565 sul router (port forwarding)
- Accedi al pannello del router (di solito da `192.168.1.1` o `192.168.0.1`)
- Cerca la sezione **Port Forwarding** o **NAT**
- Aggiungi una regola con:
  - **Porta interna**: `25565`
  - **Porta esterna**: `25565` (oppure qualsiasi altra)
  - **Protocollo**: `TCP` oppure `TCP/UDP`
  - **IP locale del tuo PC**: es. `192.168.1.118`

### 6.2 Configurazione del Firewall (Windows)
- Cerca **"Windows Defender Firewall con sicurezza avanzata"**
- Vai su **Regole in entrata → Nuova regola**
  - Tipo: **Porta**
  - Porta specifica: `25565`
  - Protocollo: TCP e UDP
  - Azione: **Consenti la connessione**


## 7. Connettersi al server
- Io stesso: `localhost:25565`
- Altri in LAN: `<IP locale del server>:25565` (ad esempio `192.168.1.118:25565`)
- Amici su Internet: `<IP pubblico del server>:25565` (ad esempio `45.123.456.78:25565`)
