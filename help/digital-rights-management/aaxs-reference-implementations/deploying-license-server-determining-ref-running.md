---
description: 'null'
seo-description: 'null'
seo-title: Kontrollerar om Reference Implementation License Server körs som den ska
title: Kontrollerar om Reference Implementation License Server körs som den ska
uuid: 84d32c94-7594-464e-a883-5338b52de2bf
translation-type: tm+mt
source-git-commit: e60d285b9e30cdd19728e3029ecda995cd100ac9

---


# Kontrollerar om Reference Implementation License Server körs som den ska {#determining-if-reference-implementation-license-server-is-running-properly}

Det finns flera sätt att avgöra om servern har startats korrekt. Det kanske inte räcker att visa loggarna eftersom licensservern loggar in på sina egna loggfiler. [!DNL catalina.log] Följ stegen nedan för att kontrollera att referensimplementeringen har startats korrekt.

* Kontrollera din [!DNL AdobeFlashAccess.log] fil. Här skriver Reference Implementation logginformation. Platsen för den här loggfilen anges av din [!DNL log4j.xml] fil och kan ändras så att den pekar på valfri plats. Som standard kommer loggfilen att skrivas ut i arbetskatalogen där du har kört Catalina.

* Navigera till följande URL: `https:///flashaccess/license/v4<your server:server port>`. Du bör se texten&quot;License Server is setup correctly&quot;.

Ett annat sätt att testa om servern körs som den ska är att paketera en del av testinnehållet, konfigurera en videospelare och spela upp den. Följande procedur beskriver processen:

1. Navigate to the [!DNL \Reference Implementation\Command Line Tools] folder. Information om hur du installerar kommandoradsverktygen finns i [Installera kommandoradsverktygen](../aaxs-reference-implementations/command-line-tools/aaxs-ref-impl-command-line-overview.md#installing-the-command-line-tools).

1. Skapa en enkel anonym princip med följande kommando:

   ```
       java -jar libs\AdobePolicyManager.jar new policy_test.pol -x
   ```

   Mer information om hur du skapar principer med Policy Manager finns i [Kommandoradsanvändning](../aaxs-reference-implementations/command-line-tools/policy-manager/command-line-usage.md).

1. Ange `encrypt.license.serverurl` egenskapen i [!DNL flashaccesstools.properties] filen som URL för licensservern (till exempel `https:// localhost:8080/`). Filen finns [!DNL flashaccesstools.properties] under [!DNL \Reference Implementation\Command Line Tools] mappen.

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

1. Kopiera de två genererade filerna till Tomcat- [!DNL webapps\ROOT\Content] mappen.
1. Navigera till `Reference Implementation\Sample Video Players\Desktop\Flash Player\Release` och kopiera innehållet till Tomcat- `webapps\ROOT\SVP\` mappen.
1. Installera Flash Player 10.1 eller senare.
1. Öppna webbläsaren och gå till följande URL:

   `https:// localhost:8080/SVP/player.html`
1. Navigera till följande URL och klicka sedan på knappen Spela upp:

   `https:// localhost:8080/Content/<your_encrypted_FLV>`
1. Om videon inte kan spelas upp kontrollerar du om några felkoder har skrivits i loggningsrutan i Sample Video Player, eller i `AdobeFlashAccess.log` filen. Platsen för `AdobeFlashAccess.log` loggfilen anges av loggfilen log4j.xml och kan ändras så att den pekar på valfri plats. Loggfilen skrivs som standard till arbetskatalogen där du har kört Catalina.
