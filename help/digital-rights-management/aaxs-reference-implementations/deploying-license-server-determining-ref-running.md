---
title: Kontrollerar om Reference Implementation License Server körs som den ska
description: Kontrollerar om Reference Implementation License Server körs som den ska
copied-description: true
exl-id: ef28e169-f8d2-4c7f-b606-aa4e811aae9b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 0%

---

# Kontrollerar om Reference Implementation License Server körs som den ska {#determining-if-reference-implementation-license-server-is-running-properly}

Det finns flera sätt att avgöra om servern har startats korrekt. Visa [!DNL catalina.log] loggarna kanske inte är tillräckliga eftersom licensservern loggar till sina egna loggfiler. Följ stegen nedan för att kontrollera att referensimplementeringen har startats korrekt.

* Kontrollera [!DNL AdobeFlashAccess.log] -fil. Här skriver Reference Implementation logginformation. Platsen för den här loggfilen anges av din [!DNL log4j.xml] och kan ändras så att den pekar på valfri plats. Som standard kommer loggfilen att skrivas ut i arbetskatalogen där du har kört Catalina.

* Navigera till följande URL: `https:///flashaccess/license/v4<your server:server port>`. Du bör se texten&quot;License Server is setup correctly&quot;.

Ett annat sätt att testa om servern körs som den ska är att paketera en del av testinnehållet, konfigurera en videospelare och spela upp den. Följande procedur beskriver processen:

1. Navigera till [!DNL \Reference Implementation\Command Line Tools] mapp. Information om hur du installerar kommandoradsverktygen finns i [Installera kommandoradsverktygen](../aaxs-reference-implementations/command-line-tools/aaxs-ref-impl-command-line-overview.md#installing-the-command-line-tools).

1. Skapa en enkel anonym princip med följande kommando:

   ```
       java -jar libs\AdobePolicyManager.jar new policy_test.pol -x
   ```

   Mer information om hur du skapar principer med Policy Manager finns i [Användning av kommandorad](../aaxs-reference-implementations/command-line-tools/policy-manager/command-line-usage.md).

1. Ange `encrypt.license.serverurl` -egenskapen i [!DNL flashaccesstools.properties] till licensserverns URL (t.ex. `https:// localhost:8080/`). The [!DNL flashaccesstools.properties] filen finns under [!DNL \Reference Implementation\Command Line Tools] mapp.

1. Paketera en del av innehållet med följande kommando:

   ```java
       java -jar libs\AdobePackager.jar  
   <i class="+ topic ph hi-d="" i "="">
   test_input_FLV  
   <i class="+ topic ph hi-d="" i "="">
   output_file  
               -p policy_test.pol 
   </i class="+ topic> 
   </i class="+ topic>
   ```

1. Kopiera de två genererade filerna till Tomcat [!DNL webapps\ROOT\Content] mapp.
1. Navigera till `Reference Implementation\Sample Video Players\Desktop\Flash Player\Release` och kopiera innehållet till Tomcat `webapps\ROOT\SVP\` mapp.
1. Installera Flash Player 10.1 eller senare.
1. Öppna webbläsaren och gå till följande URL:

   `https:// localhost:8080/SVP/player.html`
1. Navigera till följande URL och klicka sedan på knappen Spela upp:

   `https:// localhost:8080/Content/<your_encrypted_FLV>`
1. Om videon inte kan spelas upp kontrollerar du om några felkoder har skrivits i loggningsrutan i Sample Video Player, eller i `AdobeFlashAccess.log` -fil. Platsen för `AdobeFlashAccess.log` loggfilen anges av loggfilen log4j.xml och kan ändras så att den pekar på valfri plats. Loggfilen skrivs som standard till arbetskatalogen där du har kört Catalina.
