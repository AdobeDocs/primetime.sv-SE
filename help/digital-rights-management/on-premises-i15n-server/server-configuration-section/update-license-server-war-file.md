---
title: Uppdatera licensserverns WAR-fil
description: Uppdatera licensserverns WAR-fil
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 0%

---

# Uppdatera licensserverns WAR-fil{#update-the-license-server-war-file}

För att stödja klienter som har individualiserat via en On Premises Individualization-server måste du uppdatera certifikatserverns certifikatrot för tillit så att den inkluderar de nyligen förvärvade autentiseringsuppgifterna för Individualization CA. Ett Python-skript ( [!DNL addIndivCert.py]) ingår i [!DNL update_license_server] mapp.

Gör följande för att uppdatera licensservern:

1. Gör en kopia av WAR-filerna som ska uppdateras (exempel: [!DNL flashaccess.war], [!DNL faxsks.war]).
1. Kontrollera att WAR-filerna är olåsta och har behörighet att ändra dem.
1. Kör [!DNL addIndivCert.py] Python-skript för att uppdatera licensserverns WAR-filer.

   Skriptets indata är följande:

   * `cert`: PKCS12-fil som innehåller det enskilda certifikatutfärdarcertifikatet
   * `war`: WAR-fil som ska uppdateras

   Utdatafilen är en uppdaterad WAR-fil.

   ```
   ./addIndivCert.py -cert NEW_IndivCA.cer -war flashaccess.war
   ```

WAR-filerna ändras på plats. Om det behövs kan du redigera Python-skriptet så att det passar dina behov. När du har utfört uppdateringarna kan du distribuera WAR-filerna som vanligt.
