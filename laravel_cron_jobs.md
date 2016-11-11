## Impostare i cron jobs su Laravel

Reference: [https://laravel.com/docs/5.2/scheduling](https://laravel.com/docs/5.2/scheduling)

Innanzitutto, per fare che i Cron funzionino bisogna aggiungere lo scheduler di Laravel nei Cron del sistema operativo. 
Per farlo, sui sistemi Unix, bisogna usare il comando: 

```
sudo crontab -e
```

e quindi aggiungere la riga:

```
* * * * * php /path/to/artisan schedule:run >> /dev/null 2>&1
```

dove ovviamente `/path/to/artisan` è il percorso del file `artisan` nella cartella del progetto. 
Questo permetterà di eseguire il Cron sul progetto Laravel ogni minuto, poi sarà nella configurazione lato codice che si potrà impostare l'intervallo di tempo desiderato

Questa operazione dev'essere ripetuta sul server di produzione e di staging per funzionare anche in quegli ambienti
