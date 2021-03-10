---
title: Kontrollerar om Reference Implementation License Server körs som den ska
description: Kontrollerar om Reference Implementation License Server körs som den ska
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 0%

---


# Kontrollerar om Reference Implementation License Server körs korrekt {#determining-if-reference-implementation-license-server-is-running-properly}

Det finns flera sätt att avgöra om servern har startats korrekt. Det kanske inte räcker att visa [!DNL catalina.log]-loggarna eftersom licensservern loggar in på sina egna loggfiler. Följ stegen nedan för att kontrollera att referensimplementeringen har startats korrekt.

* Kontrollera din [!DNL AdobeFlashAccess.log]-fil. Här skriver Reference Implementation logginformation. Platsen för den här loggfilen anges av din [!DNL log4j.xml]-fil och kan ändras så att den pekar på valfri plats. Som standard kommer loggfilen att skrivas ut i arbetskatalogen där du har kört Catalina.

* Navigera till följande URL: `https:///flashaccess/license/v4<your server:server port>`. Du bör se texten&quot;License Server is setup correctly&quot;.

Ett annat sätt att testa om servern körs som den ska är att paketera en del av testinnehållet, konfigurera en videospelare och spela upp den. Följande procedur beskriver processen:

1. Navigera till mappen [!DNL \Reference Implementation\Command Line Tools]. Information om hur du installerar kommandoradsverktygen finns i [Installera kommandoradsverktygen](../aaxs-reference-implementations/command-line-tools/aaxs-ref-impl-command-line-overview.md#installing-the-command-line-tools).

1. Skapa en enkel anonym princip med följande kommando:

   ```
       java -jar libs\AdobePolicyManager.jar new policy_test.pol -x
   ```

   Mer information om hur du skapar principer med Policy Manager finns i [Kommandoradsanvändning](../aaxs-reference-implementations/command-line-tools/policy-manager/command-line-usage.md).

1. Ange egenskapen `encrypt.license.serverurl` i filen [!DNL flashaccesstools.properties] som URL för licensservern (till exempel `https:// localhost:8080/`). Filen [!DNL flashaccesstools.properties] finns under mappen [!DNL \Reference Implementation\Command Line Tools].

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

1. Kopiera de 2 genererade filerna till Tomcat-mappen [!DNL webapps\ROOT\Content].
1. Navigera till `Reference Implementation\Sample Video Players\Desktop\Flash Player\Release` och kopiera innehållet till mappen Tomcat `webapps\ROOT\SVP\`.
1. Installera Flash Player 10.1 eller senare.
1. Öppna webbläsaren och gå till följande URL:

   `https:// localhost:8080/SVP/player.html`
1. Navigera till följande URL och klicka sedan på knappen Spela upp:

   `https:// localhost:8080/Content/<your_encrypted_FLV>`
1. Om videon inte kan spelas upp kontrollerar du om några felkoder har skrivits i loggningsrutan i Sample Video Player eller i `AdobeFlashAccess.log`-filen. Platsen för `AdobeFlashAccess.log`-loggfilen anges av loggfilen log4j.xml och kan ändras så att den pekar på en plats som du vill. Loggfilen skrivs som standard till arbetskatalogen där du har kört Catalina.
