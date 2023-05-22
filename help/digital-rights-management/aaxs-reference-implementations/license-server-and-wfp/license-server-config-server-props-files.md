---
title: Serveregenskapsfiler
description: Serveregenskapsfiler
copied-description: true
exl-id: c42fde8f-e438-4497-bd15-ebd0f6e2eed7
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 0%

---

# Serveregenskapsfiler {#server-properties-files}

Servern kräver två konfigurationsfiler, en för licensservern och en för paketeraren. Båda filerna måste placeras i klassökvägen. Egenskapsfilerna innehåller platsen för inloggningsuppgifterna som utfärdats av Adobe. Dessa autentiseringsuppgifter kan anges som en pfx-fil och ett lösenord eller genom att ange ett alias och lösenord för en autentiseringsuppgift som lagras på en HSM.

Se egenskapsfilerna för mer information om de specifika värdena och hur respektive parameter används. Exempelegenskapsfiler finns i katalogen &quot;resources&quot; för referensimplementeringen (Reference Implementation\Server\resources).

För att säkerställa säkerheten för autentiseringsuppgiftens lösenord finns det ett verktyg (klassen ScrambleUtil.class) för att kryptera lösenordet innan det anges i filen flashaccess-refimpl.properties eller filen flashaccess-refimpl-packager.properties.

Så här förbereder du lösenordet för dina autentiseringsuppgifter:

1. Gå till [!DNL Reference Implementation\Server\refimpl\scrambler].
1. Ange kommandot från kommandotolken:

   ```
   java -classpath  
   <i class="+ topic ph hi-d="" i "="">
   path_to_adobe-flashaccess-sdk.jar.; 
        com.adobe.flashaccess.refimpl.util.ScrambleUtil " 
   <i class="+ topic ph hi-d="" i "="">
   your_pfx_password" 
   </i class="+ topic> 
   </i class="+ topic>
   ```

>[!NOTE]
>
>I föregående exempel används ett semikolon (;) som avgränsare. För andra plattformar än Microsoft Windows använder du kolon (:) som avgränsare.

Verktyget matar ut det krypterade lösenordet, som du måste kopiera till [!DNL .properties] -fil.
