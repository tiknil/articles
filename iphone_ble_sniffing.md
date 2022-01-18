# iPhone BLE Sniffing

Per eseguire lo sniff dei pacchetti BLE su iPhone per il debug della comunicazione di basso livello tra esso e un dispositivo BLE è necessario: 

1. Installare sull'iPhone un profile di debug di Apple (valido 4 giorni) con un account con Apple Developer Program attivo (seguire questa guida: [https://www.bluetooth.com/blog/a-new-way-to-debug-iosbluetooth-applications/] )
2. Scaricare su Mac l'app PacketLogger di Apple presente nel pacchetto degli Additional Tool di XCode (scaricabile da qui in base alla propria versione di XCode: [https://developer.apple.com/download/more/?=xcode])
3. Avviare PacketLogger e selezionare "File > New iOS Trace": se non compare nessun messaggio nel log significa che non si è installato il profilo correttamente
4. Avviare/Interrompere il log in base al caso d'uso da investigare, quindi esportare il log nel formato BTSnoop
5. Aprire il file esportato con Wireshark per l'analisi dei pacchetti più approfondita e con maggiori filtri di PacketLogger

- Guida Nordig per sniff ble, utile per seguire l'uso di Wireshark e l'impostazione dei filtri dello stesso: [https://cdn-learn.adafruit.com/assets/assets/000/059/041/original/nRF_Sniffer_User_Guide_v2.1.pdf?1533935335]
- Risorse utili per interpretare lo sniffing: [https://learn.adafruit.com/introducing-adafruit-ble-bluetooth-low-energy-friend/ble-sniffer]
