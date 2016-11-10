## Come mettere in produzione un backend Laravel che utilizza le "Classic API" (o NVP/SOAP API) di Paypal

Fondamentalmente bisogna predisporre 2 concetti:
1. Credenziali di accesso alle api
2. L'APP > che permette di avere l'`APP-ID` da impostare lato SDK e backend

**Prerequisiti**
* Account business PayPal verificato

### Credenziali di accesso alle api
Guida di riferimento: [https://developer.paypal.com/docs/classic/api/apiCredentials/](https://developer.paypal.com/docs/classic/api/apiCredentials/)

#### Recupero credenziali e certificato da paypal.com

* Accedi a [PayPal.com](www.paypal.com) con l'account PayPal business verificato, quindi clicca in alto a destra sull'icona del profilo e scegli "Profilo e impostazioni"
![Accedi a profilo e impostazioni dell'account](images/paypal_credentials_1.png)
* Seleziona "Strumenti di vendita" e quindi fai click su "Aggiorna" alla voce "Accesso API"
![Strumenti di vendita - Accesso API](images/paypal_credentials_2.png)
* Nella sezione "Integrazione API NVP/SOAP" fai click su "Richiedi certificato API" o "Vedi certificato API"
![Richiedi certificato API](images/paypal_credentials_3.png)
* Scarica quindi il certificato sul computer. Sarà un file `cert_key_pem.txt`
![Certificato e credenziali](images/paypal_credentials_4.png)
* Copia le credenziali nei relativi campi del file `.env` in production: 
  - valore di "Nome utente API" in env('PAYPAL_ACCOUNT_USERNAME'),
  - valore di "Password API" in env('PAYPAL_ACCOUNT_PASSWORD'),
  - valore di "Impronta digitale" in env('PAYPAL_ACCOUNT_SIGNATURE'),

#### Predisposizione certificato cifrato p12

* Aprire 


