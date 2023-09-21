---
title: Bygga AIR-programmet för Flash Access Manager
description: Bygga AIR-programmet för Flash Access Manager
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 0%

---

# Bygga AIR-programmet för Flash Access Manager {#building-the-flash-access-manager-air-application}

Om du vill skapa AIR-filen för Flash Access Manager från källkoden måste du ha Flex och AIR SDK installerade på datorn. Innan du kan paketera och köra programmet måste du kompilera MXML till en SWF-fil med [!DNL amxmlc] kompilator. The [!DNL amxmlc] kompilatorn finns i [!DNL bin] katalogen för Flex 4 eller senare SDK. Om du vill kan du ställa in systemvariabeln path så att den innehåller bin-katalogen för Flex SDK så att det blir enklare att köra verktygen på kommandoraden.

Så här skapar du AIR-filen för Flash Access Manager:

1. Öppna ett kommandoskal eller en terminal och navigera till projektmappen för AIR-programmet för Flash Access Manager ( [!DNL UI Tools\Flash Access Manager] i katalogen Reference Implementation).
1. Ange följande kommando:

   ```
   amxmlc src\FlashAccessmanager.mxml
   ```

   Körs [!DNL amxmlc] skapar [!DNL FlashAccessManager.swf], som innehåller den kompilerade koden för programmet.

Adobe AIR SDK innehåller verktyget AIR Developer Tool (ADT) för att paketera AIR-program och generera certifikat. AIR-program bör signeras digitalt. Användarna får en varning när de installerar program som inte är korrekt signerade eller som inte är signerade alls. Om du vill generera ett certifikat med kommandoraden öppnar du ett konsolfönster i samma mapp som ditt AIR-program och skriver följande:

```
adt -certificate -cn SelfSigned 1024-RSA testCert.pfx  
<i class="+ topic ph hi-d="" i "="">
  some_password 
</i class="+ topic>
```

Ersätt *some_password* med ett valfritt lösenord. Efter några sekunder bör ADT slutföra certifikatgenereringsprocessen och du bör ha en ny [!DNL testCert.pfx] i programkatalogen.

Använd sedan ADT för att paketera programmet i en [!DNL .air] med kommandot:

```
adt -package -storetype pkcs12 -keystore testCert.pfx FlashAccessManager.air src\FlashAccessManager-app.xml . -C src assets
```

Detta kommando anger för ADT att paketera programmet med hjälp av nyckelfilen i [!DNL testCert.pfx]. På raden ovan konfigurerar du ADT så att hela programmet paketeras i en fil med namnet [!DNL FlashAccessManager.air]och inkludera filerna [!DNL FlashAccessManager-app.xml] och [!DNL FlashAccessManager.swf] och bilderna från katalogen assets.

Som en del av den här processen uppmanas du att ange lösenordet som du anger för den nya certifikatfilen. Ange det, vänta ett ögonblick och [!DNL FlashAccessManager.air] -filen ska finnas i samma katalog som dina projektfiler.
