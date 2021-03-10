---
title: Exempelklientbegäranden
description: Exempelklientbegäranden
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '105'
ht-degree: 1%

---


# Exempel på klientförfrågningar{#sample-client-requests}

Du kan samla in ett bibliotek med exempelklientförfrågningar med verktyg som Charles Proxy eller Wireshark. Du bör samla in klientbegäranden efter att Individualization-servern har konfigurerats med hjälp av autentiseringsuppgifterna för Individualization Transport. Du kan sedan skicka dessa klientförfrågningar (via *curl* eller något annat verktyg) till slutpunkten för Individualization Server för att verifiera att servern fungerar som den ska. Exempel:

```
curl https://<<yourindivserver:port>>/flashaccess/i15n/v5 -­data-binary  
@sample_client_request.bin > sample_client_response.ber
```

Du kanske också vill skicka dessa begäranden igen efter att serverkonfigurationen har ändrats eller när ECI-/CRL-uppdateringarna har uppdaterats.

Du bör även uppdatera sidan för Individualiseringsstatistik på lämpligt sätt med lyckade individualiseringstransaktioner.
