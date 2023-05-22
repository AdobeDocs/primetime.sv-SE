---
title: Exempelklientbegäranden
description: Exempelklientbegäranden
copied-description: true
exl-id: 2b6a1349-aafc-4222-9081-525662f62961
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '105'
ht-degree: 0%

---

# Exempelklientbegäranden{#sample-client-requests}

Du kan samla in ett bibliotek med exempelklientförfrågningar med verktyg som Charles Proxy eller Wireshark. Du bör samla in klientbegäranden efter att Individualization-servern har konfigurerats med hjälp av autentiseringsuppgifterna för Individualization Transport. Du kan sedan skicka dessa klientförfrågningar (via *kurva* eller något annat verktyg) till slutpunkten för Individualization Server för att verifiera att servern är igång och körs som den ska. Till exempel:

```
curl https://<<yourindivserver:port>>/flashaccess/i15n/v5 -­data-binary  
@sample_client_request.bin > sample_client_response.ber
```

Du kanske också vill skicka dessa begäranden igen efter att serverkonfigurationen har ändrats eller när ECI-/CRL-uppdateringarna har uppdaterats.

Du bör även uppdatera sidan för Individualiseringsstatistik på lämpligt sätt med lyckade individualiseringstransaktioner.
