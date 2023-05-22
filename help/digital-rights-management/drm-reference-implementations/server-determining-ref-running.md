---
title: Kontrollerar om Reference Implementation License Server körs korrekt
description: Kontrollerar om Reference Implementation License Server körs korrekt
copied-description: true
exl-id: 97ca0b6c-2661-4cdc-b8d0-dcc545f009f6
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 0%

---

# Kontrollerar om Reference Implementation License Server körs korrekt {#determining-if-reference-implementation-license-server-runs-properly}

Det finns flera sätt att avgöra om din Reference Implementation License Server har startats korrekt. Du kan visa [!DNL catalina.log] loggarna kanske inte är tillräckliga eftersom licensservern loggar till sina egna loggfiler. Följ stegen nedan för att kontrollera att referensimplementeringen har startats korrekt.

* Kontrollera [!DNL AdobeFlashAccess.log] -fil. Här skriver Reference Implementation logginformation. Platsen för den här loggfilen anges av din [!DNL log4j.xml] och kan ändras så att den pekar på valfri plats. Loggfilen kopieras som standard till arbetskatalogen där du kör Catalin.

* Gå till följande URL: [!DNL https:// flashaccess/license/v4]*din server:serverport*. Du bör se texten&quot;License Server is setup correctly&quot;.

Ett annat sätt att testa om servern fungerar som den ska är att paketera ett segment i testinnehållet, konfigurera en videospelare och sedan spela upp den.

Följande procedur beskriver processen:

1. Gå till [!DNL \Reference Implementation\Command Line Tools] mapp.

   Se [Installera kommandoradsverktygen](../drm-reference-implementations/command-line-tools/install-command-line-tools.md) om hur du installerar kommandoradsverktygen.

1. Skriv följande kommando för att skapa en enkel anonym DRM-princip:

   ```
       java -jar libs\AdobePolicyManager.jar new policy_test.pol -x
   ```

   Se [Användning av kommandorad](../drm-reference-implementations/command-line-tools/configure-command-line-tools/policy-manager/policy-manager-command-line-usage.md) om hur du skapar DRM-principer med DRM Policy Manager.

1. Ange `encrypt.license.serverurl` -egenskapen i [!DNL flashaccesstools.properties] till licensserverns URL.

   Till exempel: [!DNL https:// localhost:8080/]. The [!DNL flashaccesstools.properties] filen finns i [!DNL \Reference Implementation\Command Line Tools] mapp.

1. Skriv följande kommando för att paketera ett segment av innehållet:

```
       java -jar libs\AdobePackager.jar  
       <i class="+ topic ph hi-d="" i "="">
         test_input_FLV  
        <i class="+ topic ph hi-d="" i "="">
       output_file  
               -p policy_test.pol 
       </i class="+ topic> 
       </i class="+ topic>
```

1. Kopiera de två genererade filerna till [!DNL webapps\ROOT\Content] på Tomcat-servern.
1. Gå till [!DNL Reference Implementation\Sample Video Players\Desktop\Flash Player\Release] och kopiera innehållet till [!DNL webapps\ROOT\SVP\] på Tomcat-servern.

1. Installera Flash Player version 10.1 eller senare.
1. Öppna en webbläsare och gå till följande URL: [!DNL        https:// localhost:8080/SVP/player.html]

1. Gå till följande URL och klicka sedan på **[!UICONTROL Play]**: [!DNL https:// localhost:8080/Content/] *`your_encrypted_FLV`*.

1. Om videon inte kan spelas upp kontrollerar du om några felkoder visas i loggningsrutan i Sample Video Player eller läggs till i [!DNL AdobeFlashAccess.log] -fil.

   Nu kan du söka efter platsen för [!DNL AdobeFlashAccess.log] loggfilen i log4j.xml-filen och ändra den sedan. Loggfilen kopieras som standard till arbetskatalogen där du kör Catalin.
