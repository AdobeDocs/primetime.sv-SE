---
description: 'null'
seo-description: 'null'
seo-title: Kontrollerar om Reference Implementation License Server körs korrekt
title: Kontrollerar om Reference Implementation License Server körs korrekt
uuid: afd82d6d-a11c-48ff-b48c-8f81d4b406a0
translation-type: tm+mt
source-git-commit: 19e7c941b3337c3b4d37f0b6a1350aac2ad8a0cc
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 0%

---


# Kontrollerar om Reference Implementation License Server körs korrekt {#determining-if-reference-implementation-license-server-runs-properly}

Det finns flera sätt att avgöra om din Reference Implementation License Server har startats korrekt. Du kan visa [!DNL catalina.log]-loggarna kanske inte är tillräckliga eftersom licensservern loggar till sina egna loggfiler. Följ stegen nedan för att kontrollera att referensimplementeringen har startats korrekt.

* Kontrollera din [!DNL AdobeFlashAccess.log]-fil. Här skriver Reference Implementation logginformation. Platsen för den här loggfilen anges av din [!DNL log4j.xml]-fil och kan ändras så att den pekar på valfri plats. Loggfilen kopieras som standard till arbetskatalogen där du kör Catalin.

* Gå till följande URL: [!DNL https:// flashaccess/license/v4]*din server:serverport*. Du bör se texten&quot;License Server is setup correctly&quot;.

Ett annat sätt att testa om servern fungerar som den ska är att paketera ett segment i testinnehållet, konfigurera en videospelare och sedan spela upp den.

Följande procedur beskriver processen:

1. Gå till mappen [!DNL \Reference Implementation\Command Line Tools].

   Se [Installera kommandoradsverktygen](../drm-reference-implementations/command-line-tools/install-command-line-tools.md) om hur du installerar kommandoradsverktygen.

1. Skriv följande kommando för att skapa en enkel anonym DRM-princip:

   ```
       java -jar libs\AdobePolicyManager.jar new policy_test.pol -x
   ```

   Se [Kommandoradsanvändning](../drm-reference-implementations/command-line-tools/configure-command-line-tools/policy-manager/policy-manager-command-line-usage.md) om hur du skapar DRM-principer med DRM Policy Manager.

1. Ange egenskapen `encrypt.license.serverurl` i filen [!DNL flashaccesstools.properties] som URL för licensservern.

   Exempel, [!DNL https:// localhost:8080/]. Filen [!DNL flashaccesstools.properties] finns i mappen [!DNL \Reference Implementation\Command Line Tools].

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

1. Kopiera de två genererade filerna till mappen [!DNL webapps\ROOT\Content] på Tomcat-servern.
1. Gå till katalogen [!DNL Reference Implementation\Sample Video Players\Desktop\Flash Player\Release] och kopiera innehållet till mappen [!DNL webapps\ROOT\SVP\] på Tomcat-servern.

1. Installera Flash Player version 10.1 eller senare.
1. Öppna en webbläsare och gå till följande URL: [!DNL        https:// localhost:8080/SVP/player.html]

1. Gå till följande URL och klicka sedan på **[!UICONTROL Play]**: [!DNL https:// localhost:8080/Content/] *`your_encrypted_FLV`*.

1. Om videon inte kan spelas upp kontrollerar du om några felkoder visas i loggningsrutan i Sample Video Player eller läggs till i [!DNL AdobeFlashAccess.log]-filen.

   Nu kan du söka efter platsen för [!DNL AdobeFlashAccess.log]-loggfilen i log4j.xml-filen och sedan ändra den. Loggfilen kopieras som standard till arbetskatalogen där du kör Catalin.

